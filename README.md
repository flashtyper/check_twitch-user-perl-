# check_twitch-user
small icinga/nagios script to check if a twitch user is live

Usage: 
```./check_twitch-user -u [twitchuser]-c [API Client ID] -b [full path to bearer token]```

Example:
```./check_twitch-user -u asmongold-c abcdefghijklmnopqrdtuvwqyz1234567890 -b /home/user/twitch/token```

```[twitchuser]```:
This is the login name of a twitchuser which you can easily get by (for example): 

```
curl -s --location --request GET 'https://api.twitch.tv/helix/users?login=<account name>' --header 'client-id: <client id>' --header 'Authorization: Bearer <token>'
```

```[full path to bearer token]```:
As the bearer token expire after 60 days i decided to save it in a file because i wanted to write this script as much generic as possible. 
In my case I created a cron job which requests every 30 days a new bearer token and write it into the token-file. 

Output if a user is live: 
```
Asmongold is live!

https://twitch.tv/asmongold
Titel: TBC TOURNAMENT PLANNING--HUGE 9.1 UPDATES--MOUNT TODAY 100%--GOING OVER PATCH NOTES--MAYBE A MOUNT OFF??
Game: World of Warcraft | viewer=38384
```
