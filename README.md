# check_twitch-user
small icinga/nagios script to check if a twitch user is live

Usage: 
./check_twitch-user -u [twitchuser]-c [API Client ID] -b [path to bearer token]

[twitchuser]:
This is the login name of a twitchuser which you can easily get by (for example): 
curl -s --location --request GET 'https://api.twitch.tv/helix/users?login=<account name>' --header 'client-id: <client id>' --header 'Authorization: Bearer <token>'
  

Output if a user is live: 

Asmongold ist live!

https://twitch.tv/asmongold
Titel: TBC TOURNAMENT PLANNING--HUGE 9.1 UPDATES--MOUNT TODAY 100%--GOING OVER PATCH NOTES--MAYBE A MOUNT OFF??
Game: World of Warcraft | viewer=38384
