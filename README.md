# check_twitch-user
small icinga/nagios script to check if a twitch user is live

## Usage: 

```bash
./check_twitch-user -u <twitchuser> -c <Twitch API Client ID> -b <full path to bearer token>
```

## Installation:
Just move the file into your plugin directory and add a new command and service to your icinga configuration. Don't forget to grant execution permissions. 
Maybe something like this: 
```javascript
object CheckCommand "check_twitchuser" {
  command = [ CustomPluginDir + "/twitch/check_twitchuser.pl" ]
  arguments = {
    "-u" = "$twitch_user$"
    "-c" = "client-id"
    "-b" = "/path/to/twitch/bearer/token"
  }
  vars.twitch_user = "$twitchuser$"
}
object Service "Asmongold" {
  check_command = "check_twitchuser"
  import "generic-service"
  host_name = "Twitch"
  vars.twitch_user = "asmongold"
}
```

## Output
If a streamer is live: 
```
Asmongold is live!

https://twitch.tv/asmongold
Titel: TBC TOURNAMENT PLANNING--HUGE 9.1 UPDATES--MOUNT TODAY 100%--GOING OVER PATCH NOTES--MAYBE A MOUNT OFF??
Game: World of Warcraft | viewer=38384
```
If a streamer is not live: 
```
OK - User not live | viewer=0
```

## Example:

```bash
./check_twitch-user -u asmongold -c abcdefghijklmnopqrdtuvwqyz1234567890 -b /path/to/twitch/bearer/token
```

## Get streamers login name
```bash
curl -s --location --request GET 'https://api.twitch.tv/helix/users?login=<account name>' --header 'client-id: <client id>' --header 'Authorization: Bearer <token>'
```

## Why should i save my bearer token in a file? 
As the bearer token expire after 60 days i decided to save it in a file because i wanted to write this script as much generic as possible. 
In my case I created a cron job which requests every 30 days a new bearer token and write it into the token-file. Another benefit is that you can use your bearer file for other scripts and api calls. 
