## ansible-bootstrap-server

[![Build status](https://api.travis-ci.org/tasdikrahman/ansible-bootstrap-server.svg)](https://travis-ci.org/tasdikrahman/ansible-bootstrap-server) 

Targets Debian and RHEL based systems

- bootstrap-server:
	
	Currently, it has `roles` for 

	- `update` : update the apt-cache and upgrades it
	- `install-minimal-packages` : Installs some bare bones apt-packages
	- `create-new-user`: Creates a new user called `{{ username }}` (specified inside the `defaults/main.yml`) and copies the host's `.ssh/id_rsa` over to the new user's `.ssh` dir and adds this user to the `sudoers` list
		- specify your hashed password inside the file `roles/create_new_user/defaults/main.yml`
		- generate your hashed password using 

	```python
	python -c 'import crypt; print crypt.crypt("<your-password>", "<your-key>")'
	```

	- `basic-server-hardening`:
		- Disallow root SSH access
		- Disallow password authentication
		- Enable a basic firewall (`ufw` in this case )
	- `vimrc-server-flavor`: places the `.vimrc` server taken from my dotfiles and places it into the `~/.vimrc` for the user `{{ usnername }}`
	- `pip`
		- Installs `pip` and `mkvirtualenv` for managing python virtual environments

## Running it

**NOTE**: You need to have `sshpass` on your machine. [Ref](https://gist.github.com/arunoda/7790979)

For Mac

- `brew install https://raw.githubusercontent.com/kadwanev/bigboybrew/master/Library/Formula/sshpass.rb`

For Debian based systems

- `apt-get install sshpass`

```bash
$ cp inventory.example inventory
$ cat inventory.example
[remotenode]
<ip-addr>

[all:vars]
ansible_connection=ssh
ansible_ssh_user=root
ansible_ssh_pass=<your-pass>
```

If everything is good, check the ssh connection once

```bash
$ ansible -m ping -i inventory remotenode
<ip-addr> | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
```

Change the variable in `play.yml` named `your-username` with the new user that you want to create

```bash
$ ansible-playbook play.yml -i inventory -vvv
```

## LICENSE

GPLv3

## Donation 

If you have found my little bits of software being of any use to you, do consider helping me pay my internet bills :)


| PayPal | <a href="https://paypal.me/tasdik" target="_blank"><img src="https://www.paypalobjects.com/webstatic/mktg/logo/AM_mc_vs_dc_ae.jpg" alt="Donate via PayPal!" title="Donate via PayPal!" /></a> |
|:-------------------------------------------:|:-------------------------------------------------------------:|
| Gratipay  | <a href="https://gratipay.com/tasdikrahman/" target="_blank"><img src="https://cdn.rawgit.com/gratipay/gratipay-badge/2.3.0/dist/gratipay.png" alt="Support via Gratipay" title="Support via Gratipay" /></a> |
| Patreon | <a href="https://www.patreon.com/tasdikrahman" target="_blank"><img src="http://i.imgur.com/ICWPFOs.png" alt="Support me on Patreon" title="Support me on Patreon" /></a> |
| £ (GBP) | <a href="https://transferwise.com/pay/d804d854-6862-4127-afdd-4687d64cbd28" target="_blank"><img src="http://i.imgur.com/ARJfowA.png" alt="Donate via TransferWise!" title="Donate via TransferWise!" /></a> |
| € Euros | <a href="https://transferwise.com/pay/64c586e3-ec99-4be8-af0b-59241f7b9b79" target="_blank"><img src="http://i.imgur.com/ARJfowA.png" alt="Donate via TransferWise!" title="Donate via TransferWise!" /></a> |
| ₹ (INR)  | <a href="https://www.instamojo.com/@tasdikrahman" target="_blank"><img src="https://www.soldermall.com/images/pic-online-payment.jpg" alt="Donate via instamojo" title="Donate via instamojo" /></a> |
