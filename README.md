# check_postfix_alive

Nagios/Icinga check for recent successful transactions in the Postfix maillog

 * -w warning time (minutes, default 60)
 * -c critical time (minutes, default 180) 
 * -r only check internally relayed mail (optional)
 * -x only check external smtp mail (not internally relayed) (optional)
 * -i Regex: Pattern to identify internal delivery (required with -r or -x)
 * -l Logfile (default: /var/log/maillog, /var/log/mail.log, /var/log/mail.info)
 * -t timezone of time stamps in logfile (optional)
 * -a anonymize mail addresses in output (optional)

For log rotation, the script looks for a previous generation of the log (*.1), which must not be compressed.

# Examples

Check for recently incoming (-i) mail, identified by the next hop being "dovecot":

```
command[check_postfix_delivery]=/opt/PostfixAlive/check_postfix_alive -r -i 'dovecot' -a
```

Check for recently outgoing (-x) mail, with incoming mail excluded by the next hop being "dovecot":

```
command[check_postfix_outbound]=/opt/PostfixAlive/check_postfix_alive -x -i 'dovecot' -a
```
