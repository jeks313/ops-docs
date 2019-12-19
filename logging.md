# Why

Logging forms the basis of all subsequent observability practices - from logging to metrics and on to tracing, good clear logging provides the base upon which decisions can be made on what is meaningful for your particular service.
Logging provides living documentation on what your service does, is currently doing, and the issues it is encountering. It should enable operators of the service to discover what the service does, what it is doing currently. 
My experience running thousands of micro-services has shown that clear and robust logging is one of the primary indicators of the maturity of a service and it's ease of implementation and support.

# How To Log

## Log something!

If you are doing work, I expect you to log about the work being done. For what you should log see below.
If you think logging each action taken is too verbose, log a summary of actions per time period. When I open and tail a log for your service I should be able to tell it is operating. Only logging errors is not correct.

## Structured
Use JSON. Period.
If you must use text (but really, do not, please!):
No multi-line logging. Ever. Really, this is evil. Yes, looking at you, Java stack traces.
Key/Value pairs can be made in text logs to include the context and other values.
Hybrid log if you must - include unstructured text, but also include key/value pairs or JSON as part of the line.

## Context

- Always include context when you instantiate the logger. Include on every line/log:
- Date / time. Use ISO standard date formats RFC3339 / ISO8601 in UTC is the only acceptable format. No, 05/15/19 is not a good date format.

Example bad date format from our logs with no timezone, so this is an ambiguous time.

```
2019-12-10 06:55:51.770 ERROR SomeExceptionMiddlewareHandler - Some Exception caught during processing
```

- Request ID and user context. Include context that ties log lines for a single request together, include context that ties requests for a single session together, include context that ties requests for a single user together. Include all 3 - logging wizardry!
- Application Context. Include context under which your application is running, pod name, server name, for example. Good logging systems might add this for you, but might not.
- Code context, include file, function, and line. Be succinct though - no full filesystem paths on every line please! Best practice would see this included on non-happy path code paths - so errors, and failure events. Be mindful of the size of your log line.

## Stdout / Stderr

This is the only acceptable log output stream. Do not log to files, especially your own log files. If required provide a syslog functionality.

# What To Log

## Logging Dos 

Log as if your program was writing a journal of its lifetime: it’s starts, it handles life events, each life event has major branching/decision points, things that happen, major events that occur, and failures along the way. Logging should always indicate both healthy

- Startup

As you start in life, getting ready to serve others, log your environment. What are you configured to talk to, what does that resolve to, what are your dependencies that you need, are they healthy, are there any environment variables that change your operation, etc. This information should also be available in the /health endpoint of your service, indicating your current running environment and current external dependencies.

- Events

These are actions that have occurred that change state; a pure data accessor service can decide to log access if and only if there is something that differs between such accesses. Otherwise access logs are sufficient.

- Decisions

Log the major decision points. If there is a branch where different actions are taken based on input data, these should be logged. A new service will log all decisions, a mature service can start eliminating the common path decisions that are the default most of the time.
Example: a data accessor service would log decisions to deny access and include why.

- Errors

Log any errors that have occurred. Errors are unrecoverable events that have happened - ones that mean you could not take the action requested by the consumer of the service. All errors should also be metrics. Logs are a way to include more in-depth reasons and context around the error.
Errors should be actionable. The operator should be able to do something to address the error, or the error should indicate a bug in the software.

Do not just log an exception! You must log context to that exception - why this is considered a failure, context on the failure be that a message ID, device ID, customer ID, etc.
Errors should result in a 500 series return result in API code. If you log an error, but return a success level error code, this is not an error, this is a metric only. These might be considered for inclusion into an SLO.
Strive for the zen state of Error Zero. This is when your service in, normal trouble-free operation, logs no errors. There is no such thing as a "normal" error. Do you get bad input? Handle this and increment a metric, do not log a JSON parse exception to the logs. Each exception logged under Error Zero should be treated as a bug and either fixed, handled gracefully, and / or converted to a metric. Once this is done that log can be converted to INFO, context added, and the exception removed, returning you to the Error Zero state.

- Dependencies

When a service is dependent on external entities or services, logs should include this fact, include completion timing, and include these completion times as metrics.

## Logging Do NOTs

- Log sensitive data, such as passwords and PII
- Log excessively for regular operation. Remember this service could be hit millions of times, regular operation should create the minimal footprint for the happy path. Happy path execution should create a minimal footprint outside of events, decisions and errors. Enough to know something happened, but not a blow by blow on the happy path please.
- If events are numbered in the 100's of millions, it is acceptable to log a summary roll up of events per time period, but events (and thus activity) must be logged.
- Log exceptions with no context.
- Log warnings, or WARN level
These should never be present in production quality code. Why? These are developer todo lists in log file form. What are warnings? Something bad, that’s not quite an error? Do you want someone to take action on this message? If so it’s an error, if not, it’s informational. If it caused the user to fail, it’s an error. If it did not it’s informational. As a developer do you want to know when that happens, and how often? Create a log event with a metric that you can visualize and get alerted on. Include it in your SLO. So, warnings are work that has not be completed yet, and a warning that the service is not ready.
- Errors, Warnings, Info, Trace
-- Errors
-- Warnings
These should never be present in production quality code. Why? These are developer todo lists in log file form. What are warnings? Something bad, that’s not quite an error? Do you want someone to take action on this message? If so it’s an error, if not, it’s informational. If it caused the user to fail, it’s an error. If it did not it’s informational. As a developer do you want to know when that happens, and how often? Create a log event with a metric that you can visualize and get alerted on. Include it in your SLO. So, warnings are work that has not be completed yet, and a warning that the service is not ready.
- Results
Return code, HTTP response code, timing

# Where To Log

Stdout/Stderr. This is the only place to write logs.
OK, OK, syslog is fine in a pinch.
No, no, no, don’t write to files. Why not? Because these now need management, rotation, compaction, knowledge of your location is needed outside your service, so the orchestration system needs to know, it’s just … bad.
But … but … I can only write to a file! Really, I would consider this a broken service. But. If you must ... then include a sidecar logging service that has knowledge of where you log, cleans up your mess, and sends logs to where they should be. These are your responsibility, clean up your room, don’t ask others to do it for you.

# Metrics
Errors
Warnings
Decisions

Log Scoring - How Am I Doing?
(work in progress, just an idea on how to assess or rank a service)

What
0 points - I don’t log in my application. I just use a debugger if something goes wrong!
1 point - I log, it’s text, and unstructured.
2 points - I log to a file, it’s text but includes some context
3 points - I log to a file, it’s text but includes JSON context fields (hybrid logging)
5 points - I log to a file, it’s in JSON
10 points - I log to stdout and let my orchestration layer handle logs, it's all JSON

Where
0 points - I log to a file
2 points - I log to syslog
5 points - I log to stdout/stderr
