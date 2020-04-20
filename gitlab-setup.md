GitLab can be installed via either as Complete Monolith Binary in a Server or as Container.

Here we will go through monolithic approch.

It uses 
* nginx as web server, 
* postgresql as backend and 
* Ruby-On-Rails framework.
All of these along with other components are tied together in the single binary.

## Step 1:
As of now, Gitlab can be run over http and https (prefereable).
Https requires FQDN (Fully Qualified Domain Name). So, it has to be setup first.
Use `hostnamectl set-hostname <<your_preferred_hostname>>` command to set a hostname and use `hostnamectl` to verify. Remember always provide FQDN in order to remove conflicts.

## Step 2: 
If you are using https, then Gitlab requires SSL certificates for authentication. Self signed certificates issued via openssl will only work inside the server. Outside, it requires third party issued SSL certificates.

## Step 3:
Go to https://about.gitlab.com/install/#ubuntu & follow instructions.

## Step 4:
Gitlab commands to remember:
`
sudo gitlab-ctl start
sudo gitlab-ctl stop
sudo gitlab-ctl restart
sudo gitlab-ctl status
sudo gitlab-ctl reconfigure
`
Individual gitlab components can also be managed as `sudo gitlab-ctl nginx <<status/start/stop/restart>>`

## Step 5:
Go to /etc/gitlab/gitlab.rb. Use vim to open it and make necessary changes in SSL section as stated below.
`
nginx['redirect_http_to_https'] = true
nginx['ssl_certificate'] = "path-to-fullchain.pem"
nginx['ssl_certificate_key'] = "path-to-privkey.pem"
`
Or,
go to /etc/gitlab/ssl/ and check for ssl files. Download your certificates and rename them as required and replace them in the folder.

Run command `sudo gitlab-ctl reconfigure` to reconfigure.


## Step 6:

Also there is mail server configuration to be done in order to push mail notifications.

gitlab_rails['smtp_enable'] = true
gitlab_rails['smtp_address'] = "your-mail-domain"
gitlab_rails['smtp_port'] = your-mail-port
gitlab_rails['smtp_user_name'] = "username"
gitlab_rails['smtp_password'] = "password"
gitlab_rails['smtp_domain'] = "your-domain"
gitlab_rails['smtp_authentication'] = "login"
gitlab_rails['smtp_enable_starttls_auto'] = true
gitlab_rails['smtp_tls'] = true

Run command `sudo gitlab-ctl reconfigure` to reconfigure.

## Troubleshoot:

* Resetting root password:

https://docs.gitlab.com/ee/security/reset_root_password.html

To reset your root password, first log into your server with root privileges.

Start a Ruby on Rails console with this command:

`gitlab-rails console -e production`

Wait until the console has loaded.

There are multiple ways to find your user. You can search for email or username.

`user = User.where(id: 1).first`

Now you can change your password:

`user.password = 'secret_pass'`
`user.password_confirmation = 'secret_pass'`

It’s important that you change both password and password_confirmation to make it work.

Don’t forget to save the changes.

`user.save!`

Exit the console and try to login with your new password.