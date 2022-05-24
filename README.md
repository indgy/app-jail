# App Jail
A Bastille template to create the mimimal possible jail to run a binary application

## Usage
Create an app jail

```bastille create -E [your_jail_name]```

Copy this template to your machine 

```bastille bootstrap http://github.com/indgy/app-jail```

Then apply it to your jail

```bastille template [your_jail_name] indgy/app-jail```
