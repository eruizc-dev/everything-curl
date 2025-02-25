# --write-out

`--write-out` or just `-w` for short, outputs text and information after a
transfer is completed. It offers a large range of variables that you can
include in the output, variables that have been set with values and
information from the transfer.

Instruct curl to output a string by passing plain text to this option:

    curl -w "formatted string" http://example.com/

…and you can also have curl read that string from a given file instead if
you prefix the string with '@':

    curl -w @filename http://example.com/

…or even have curl read the string from stdin if you use '-' as filename:

    curl -w @- http://example.com/

The variables that are available are accessed by writing `%{variable_name}` in
the string and that variable will then be substituted by the correct value. To
output a normal '%' you just write it as '%%'. You can also output a newline
by using '\n', a carriage return with '\r' and a tab space with '\t'.

(The %-symbol is special on the Windows command line, where all occurrences of
% must be doubled when using this option.)

As an example, we can output the Content-Type and the response code from an
HTTP transfer, separated with newlines and some extra text like this:

    curl -w "Type: %{content_type}\nCode: %{response_code}\n" http://example.com

This feature writes the output to stdout so you probably want to make sure
that you do not also send the downloaded content to stdout as then you might
have a hard time to separate out the data.

## Available --write-out variables

Some of these variables are not available in really old curl versions.

| Variable             | Description                                                                           |
|----------------------|---------------------------------------------------------------------------------------|
| `content_type`       | Content-Type of the requested document, if there was any.                             |
| `errormsg`           | Error message from the transfer. Empty if no error occurred. (Introduced in 7.75.0)   |
| `exitcode`           | Numerical exit code from the transfer. 0 if no error occurred. (Introduced in 7.75.0) |
| `filename_effective` | The ultimate filename that curl writes out to. Practical if curl is told to write to a file with the `--remote-name` or `--output` option. It's most useful in combination with the `--remote-header-name` option.|
| `ftp_entry_path` | The initial path curl ended up in when logging on to the remote FTP server.                      |
| `http_code`     | The former variable name for what is now known as `response_code`.                               |
| `http_connect`   | the numerical code that was found in the last response (from a proxy) to a curl CONNECT request. |
| `http_version`   | The http version that was used.                                                                  |
| `json`           | all write-out variables as a single JSON object.                                                 |
| `local_ip` | IP address of the local end of the most recently used connection - can be either IPv4 or IPv6 |
| `local_port` | Local port number of the most recently used connection |
| `method` | HTTP method the most recent request used | 
| `num_connects` | Number of new connects made in the recent transfer. |
| `num_headers` | Number of response headers in the last response |
| `num_redirects` | Number of redirects that were followed in the request. |
| `onerror` | If the transfer ended with an error, show the rest of the string, otherwise stop here. (Introduced in 7.75.0) |
| `proxy_ssl_verify_result`| The result of the SSL peer certificate verification that was requested when communicating with a proxy. 0 means the verification was successful. |
| `redirect_url` | The actual URL a redirect *would* take you to when an HTTP request was made without `-L` to follow redirects. |
| `remote_ip` | The remote IP address of the most recently used connection — can be either IPv4 or IPv6. |
| `remote_port`| The remote port number of the most recently made connection. |
| `response_code` | The numerical response code that was found in the last transfer. |
| `scheme` | scheme used in the previous URL |
| `size_download` | Total number of bytes that were downloaded. |
| `size_header` | Total number of bytes of the downloaded headers. |
| `size_request` | Total number of bytes that were sent in the HTTP request.
| `size_upload` | Total number of bytes that were uploaded. |
| `speed_download` | Average download speed that curl measured for the complete download in bytes per second. |
| `speed_upload` | Average upload speed that curl measured for the complete upload in bytes per second.|
| `ssl_verify_result` | the result of the SSL peer certificate verification that was requested. 0 means the verification was successful.
| `stderr` | Makes the rest of the output get written to stderr.
| `stdout` | makes the rest of the output get written to stdout.
| `time_appconnect` | The time in seconds, it took from the start until the SSL/SSH/etc connect/handshake to the remote host was completed. |
| `time_connect`| The time in seconds, it took from the start until the TCP connect to the remote host (or proxy) was completed. |
| `time_namelookup` | The time in seconds, it took from the start until the name resolving was completed. | 
| `time_pretransfer` | The time in seconds, it took from the start   until the file transfer was just about to begin. This includes all pre-transfer commands and negotiations that are specific to the particular protocol(s) involved. |
| `time_redirect` | The time in seconds, it took for all redirection steps including name lookup, connect, pre-transfer and transfer before the final transaction was started. time_redirect the complete execution time for multiple redirections. |
| `time_starttransfer` | The time in seconds, it took from the start until the first byte was just about to be transferred. This includes time_pretransfer and also the time the server needed to calculate the result.|
| `time_total` | The total time in seconds, that the full operation lasted. The time will be displayed with millisecond resolution.|
| `url` | The URL used in the transfer. (Introduced in 7.75.0)|
| `url_effective` | The URL that was fetched last. This is particularly meaningful if you have told curl to follow Location: headers (with `-L`).
| `urlnum` | 0-based numerical index of the URL used in the transfer. (Introduced in 7.75.0)
