### Exercise 2: User and Group Management

1. Create a new user called devops_user and assign them to a group called devops.

**	sudo addgroup devops
	sudo adduser devops_user --ingroup devops

2. Set a password for the user and ensure they are required to change it after the first login.

**	sudo chage -d 0 devops_user

3. Add the user devops_user to the sudoers file, so they can run commands with superuser privileges.

**	sudo usermod -aG sudo devops_user

4. Create another user called intern_user and add them to the devops group.

**	sudo adduser intern --ingroup devops

5. Verify that both users are in the devops group by checking the group membership.

**	groups devops_user

        groups intern
