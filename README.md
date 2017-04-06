## ansible-bootstrap-server

- bootstrap-server:
	
	Currently, it has `roles` for 

	- `update` : update the apt-cache and upgrades it
	- `install_minimal_packages` : Installs some bare bones apt-packages
	- `create_new_user`: Creates a new user called `{{ username }}` (specified inside the `defaults/main.yml`) and copies the host's `.ssh/id_rsa` over to the new user's `.ssh` dir and adds this user to the `sudoers` list
		- specify your hashed password inside the file `roles/create_new_user/defaults/main.yml`
		- generate your hashed password using 

	```python
	python -c 'import crypt; print crypt.crypt("<your-password>", "<your-key>")'
	```

	- `basic_server_hardening`:
		- Disallow root SSH access
		- Disallow password authentication
		- Enable a basic firewall (`ufw` in this case )
	- `vimserver`: places the `.vimrc` server taken from my dotfiles and places it into the `~/.vimrc` for the user `{{ usnername }}`


## LICENSE

GPLv3
