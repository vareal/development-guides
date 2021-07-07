In your terminal:
```ruby
scp username@remotehost.com:file_name.txt /path/to/local
```

replacing the username, remotehost(remotehost may be replaced by ip address), remote file_name, and local directory as appropriate.

If you want to access EC2 (or other service that requires authenticating with a private key), use the -i option:
```ruby
scp -i /path/to/local/key_file.pem username@remotehost.edu:/remote/dir/file_name.txt /path/to/local
```

Example:
```ruby
sudo scp -i /home/hien/Documents/pg_production.pem ubuntu@[ip address]:/webapp/mydomain.com/shared/log/sidekiq.log /home/hien/Desktop
```
*note:* -i is for the identity_file
