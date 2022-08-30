# Front-project

Project to practice HTML/CSS/JavaScript skills

## Goals
- HTML - create an html page to display a table with a list of accounts.
- CSS - visualize page.
- Javascript - generate basic CRUD (create, read, update, delete) operations based on provided api. Validate input data.



## To run project

1. Download Tomcat(version 9 - Important) : https://tomcat.apache.org/download-90.cgi.
2. Set up the launch of the application through the Idea: Alt + Shift + F9 -> Edit Configurations… -> Alt + insert -> tom (in the search bar) -> Local.



- After that, you need to click CONFIGURE and indicate where the archive with Tomcat was downloaded and unpacked.



- In the Deployment tab: Alt + insert -> Artifact… -> rpg:war exploded -> OK.
- Leave only / (forward slash) in the Application context: field.



- Click APPLY.
- Close the settings window.

3. Launch the application. To do this: Alt + Shift + F9 -> (config name, I named it 'App') -> Run.
4. After deploying the application, a new tab will open in the browser selected during configuration.

## Api

### Get players list
```
URL -	/rest/players
Method -	Optional: Integer pageNumber, Integer pageSize
Data Params -	None
Success Response - Code: 200 OK
Content: [
 {
  “id”:[Long],
  “name”:[String],
  “title”:[String],
  “race”:[Race],
  “profession”:[Profession],
  “birthday”:[Long],
  “banned”:[Boolean],
  “level”:[Integer]
 },
 …
]

Notes

- pageNumber – a parameter that is responsible for the number of the displayed page when using paging.
The numbering starts from zero.

- pageSize – parameter that is responsible for the number of results on one page when paging.

public enum Race {
    HUMAN,
    DWARF,
    ELF,
    GIANT,
    ORC,
    TROLL,
    HOBBIT
}

public enum Profession {
    WARRIOR,
    ROGUE,
    SORCERER,
    CLERIC,
    PALADIN,
    NAZGUL,
    WARLOCK,
    DRUID
}
```
### Get players count
```
URL	- /rest/players/count
Method -	GET
URL Params -	None
Data Params -	None
Success Response	- Code: 200 OK
Content: Integer
```
### Delete player
```
URL - /rest/players/{id}
Method - DELETE
URL Params -	id
Data Params - None
Success Response -	Code: 200 OK

Notes	

- If the player is not found - response with an error code 404.

- If the id value is not valid, the response will be an error with a 400 code.
```
### Update player
```
URL	- /rest/players/{id}
Method -	POST
URL Params -	id
Data Params:	
{
  “name”:[String],       --optional
  “title”:[String],     --optional
  “race”:[Race], --optional
  “profession”:[Profession], --optional
  “banned”:[Boolean]    --optional
}

Success Response - Code: 200 OK
Content: {
  “id”:[Long],
  “name”:[String],
  “title”:[String],
  “race”:[Race],
  “profession”:[Profession],
  “birthday”:[Long],
  “banned”:[Boolean],
  “level”:[Integer]
 }
 
Notes	
- Only fields that are not null are updated.

- If the player is not found in the database, the response is an error with the 404 code.

- If the id value is not valid, the response is an error with a 400 code.
```
### Create player
```
URL -	/rest/players
Method -	POST
URL Params -	None
Data Params:	
{
  “name”:[String],
  “title”:[String],
  “race”:[Race],
  “profession”:[Profession],
  “birthday”:[Long],
  “banned”:[Boolean], --optional, default=false
  “level”:[Integer]
}
Success Response - Code: 200 OK
Content: {
  “id”:[Long],
  “name”:[String],
  “title”:[String],
  “race”:[Race],
  “profession”:[Profession],
  “birthday”:[Long],
  “banned”:[Boolean],
  “level”:[Integer]
 },
 
Notes	

We cannot create a player if:

- not all parameters from Data Params are specified (except for banned);
- the length of the “name” or “title” parameter value exceeds the size of the corresponding field (12 and 30 characters);
- the value of the “name” parameter is an empty string;
- the level is outside the specified limits (from 0 to 100);
- birthday:[Long] < 0;
- date of registration are outside the specified limits.
- In the case of all of the above, the response is an error with a 400 code.
```