#### [Home](../README.md)
## Bashbot function reference

### Send, forward, delete messages

##### send_action
```send_action``` shows users what your bot is currently doing.

*usage:* send_action "${CHAT[ID]}" "action"

*"action":* ```typing```, ```upload_photo```, ```record_video```, ```upload_video```, ```record_audio```, ```upload_audio```, ```upload_document```, ```find_location```.

*alias:* _action "action"

*example:* 
```bash
send_action "${CHAT[ID]}" "typing"
send_action "${CHAT[ID]}" "record_audio"
```


##### send_normal_message
```send_normal_message``` sends text only messages to the given chat.

*usage:*  send_normal_message "${CHAT[ID]}" "message"

*alias:* _normal_message "message"

*example:* 
```bash
send_normal_message "${CHAT[ID]}" "this is a text message"
```


##### send_markdown_message
```send_markdown_message``` sends markdown style messages to the given chat.
Telegram supports a [reduced set of Markdown](https://core.telegram.org/bots/api#markdown-style) only

*usage:* send_markdown_message "${CHAT[ID]}" "markdown message"

*alias:* _markdown "message"

*example:* 
```bash
send_markdown_message "${CHAT[ID]}" "this is a markdown  message, next word is *bold*"
send_markdown_message "${CHAT[ID]}" "*bold* _italic_ [text](link)"
```

##### send_html_message
```send_html_message``` sends HTML style messages to the given chat.
Telegram supports a [reduced set of HTML](https://core.telegram.org/bots/api#html-style) only

*usage:* send_html_message "${CHAT[ID]}" "html message" 

*alias:* _html_message "message"

*example:* 
```bash
send_normal_message "${CHAT[ID]}" "this is a markdown  message, next word is <b>bold</b>"
send_normal_message "${CHAT[ID]}" "<b>bold</b> <i>italic><i> <em>italic>/em> <a href="link">Text</a>"
```

##### forward_message
```forward_mesage``` forwards a messsage to the given chat.

*usage:* forward_message "chat_to" "chat_from" "${MESSAGE[ID]}"

*old call:* forward "${CHAT[ID]}" "$FROMCHAT" "${MESSAGE[ID]}"

*alias:* _forward "$FROMCHAT" "${MESSAGE[ID]}"

See also [Text formating options](https://core.telegram.org/bots/api#formatting-options)

----

##### delete_message
If your Bot is admin of a Chat he can delete every message, if not he can delete only his messages.

*usage:* delete_message "${CHAT[ID]}" "${MESSAGE[ID]}"

*alias:* _del_message "${MESSAGE[ID]}"

See also [deleteMessage limitations](https://core.telegram.org/bots/api#deletemessage)

----

### File, Location, Venue, Keyboard 


##### send_file
send_file allows you to send different type's of files, e.g. photos, stickers, audio, media, etc. [see more](https://core.telegram.org/bots/api#sending-files)

*usage:* send_file "${CHAT[ID]}" "file" "caption"

*example:* 
```bash
send_file "${CHAT[ID]}" "/home/user/doge.jpg" "Lool"
send_file "${CHAT[ID]}" "https://www.domain,com/something.gif" "Something"
```

##### send_location
*usage:* send_location "${CHAT[ID]}" "Latitude" "Longitude"


##### send_venue
*usage:* send_venue "${CHAT[ID]}" "Latitude" "Longitude" "Title" "Address" "foursquare id (optional)"


----

##### send_keyboard
Note: since version 0.6 send_keyboard was changed to use native "JSON Array" notation as used from Telegram. Example Keybord Array definitions:

- yes no in two rows:
    - OLD format: 'yes' 'no' (two strings)
    - NEW format: '[ "yes" ] , [ "no" ]' (two arrays with a string)
- new layouts made easy with NEW format:
    - Yes No in one row: '[ "yes" , "no" ]'
    - Yes No plus Maybe in 2.row: '[ "yes" , "no" ] , [ "maybe" ]' 
    - numpad style keyboard: '[ "1" , "2" , "3" ] , [ "4" , "5" , "6" ] , [ "7" , "8" , "9" ] , [ "0" ]'

*usage:*  send_keyboard "chat-id" "message" "keyboard"

*alias:* _keyboard "message" "keyboard"

*example:* 
```bash
send_keyboard "${CHAT[ID]}" "Say yes or no" "[ \\"yes\" , \\"no\" ]""
send_keyboard "${CHAT[ID]}" "Say yes or no" "[ \\"yes\\" ] , [ \\"no\\" ]"
send_keyboard "${CHAT[ID]}" "Enter digit" "[ \\"1\\" , \\"2\\" , \\"3\\" ] , [ \\"4\\" , \\"5\\" , \\"6\\" ] , [ \\"7\\" , \\"8\\" , \\"9\\" ] , [ \\"0\\" ]"
```

##### remove_keyboard
*usage:* remove_keybord "$CHAT[ID]" "message"

*alias:* _del_keyboard "message"

*See also: [Keyboard Markup](https://core.telegram.org/bots/api/#replykeyboardmarkup)*

----

##### send_button
*usage:*  send_button "chat-id" "message" "text" "URL"

*alias:* _button "text" "URL"

*example:* 
```bash
send_button "${CHAT[ID]}" "MAKE MONEY FAST!!!" "Visit my Shop" "https://dealz.rrr.de"
```

##### send_inline_keyboard
This allows to place multiple inline buttons in a row. The inline buttons must specified as a JSON array in the following format:

```[ {"text":"text1", "url":"url1"}, ... {"text":"textN", "url":"urlN"} ]```

Each button consists of a pair of text and URL values, sourrounded by '{ }', multiple buttons are seperated by '**,**' and everthing is wrapped in '[ ]'.

*usage:*  send_inline_keyboard "chat-id" "message" "[ {"text":"text", "url":"url"} ...]"

*alias:* _inline_keyboard "[{"text":"text", "url":"url"} ...]"

*example:* 
```bash
send_inline_keyboard "${CHAT[ID]}" "MAKE MONEY FAST!!!" '[{"text":"Visit my Shop", url"":"https://dealz.rrr.de"}]'
send_inline_keyboard "${CHAT[ID]}" "" '[{"text":"button 1", url"":"url 1"}, {"text":"button 2", url"":"url 2"} ]'
send_inline_keyboard "${CHAT[ID]}" "" '[{"text":"b 1", url"":"u 1"}, {"text":"b 2", url"":"u 2"}, {"text":"b 2", url"":"u 2"} ]'
```

*See also [Inline keyboard markup](https://core.telegram.org/bots/api/#inlinekeyboardmarkup)*

----

### User Access Control

##### kick_chat_member
If your Bot is a chat admin he can kick and ban a user.

*usage:* kick_chat_member "${CHAT[ID]}" "${USER[ID]}"

*alias:* _kick_user "${USER[ID]}"

##### unban_chat_member
If your Bot is a chat admine can unban a kicked user.

*usage:*  unban_chat_member "${CHAT[ID]}" "${USER[ID]}"

*alias:* _unban "${USER[ID]}"

##### leave_chat
Your Bot will leave the chat.

*usage:* leave_chat "${CHAT[ID]}"

*alias:* _leave 

```bash
if _is_admin ; then 
 send_markdown_message "${CHAT[ID]}" "*LEAVING CHAT...*"
 leave_chat "${CHAT[ID]}"
fi
```

'See also [kick Chat Member](https://core.telegram.org/bots/api/#kickchatmember)*

----

##### user_is_botadmin
Return true (0) if user is admin of bot, user id if botadmin is read from file './botadmin'.

*usage:*  user_is_botadmin "${USER[ID]}"

*alias:* _is_botadmin 

*example:* 
```bash
 _is_botadmin && send_markdown_message "${CHAT[ID]}" "You are *BOTADMIN*."
```

##### user_is_creator
Return true (0) if user is creator of given chat or chat is a private chat.

*usage:* user_is_creator "${CHAT[ID]}" "${USER[ID]}"

*alias:* _is_creator

##### user_is_admin
Return true (0) if user is admin or creator of given chat.
 
*usage:* user_is_admin "${CHAT[ID]}" "${USER[ID]}"

*alias:* _is_admin

*example:* 
```bash
if _is_admin ; then 
  send_markdown_message "${CHAT[ID]}" "*LEAVING CHAT...*"
  leave_chat "${CHAT[ID]}"
fi
```

*See also [Chat Member](https://core.telegram.org/bots/api/#chatmember)*

##### user_is_allowed
Bahsbot supports User Access Control, see [Advanced Usage](3_advanced.md)

*usage:* user_is_allowed "${USER[ID]}" "what" "${CHAT[ID]}"

*example:* 
```bash
if ! user_is_allowed "${USER[ID]}" "start" "${CHAT[ID]}" ; then
  send_normal_message "${CHAT[ID]}" "You are not allowed to start Bot."
fi
```

----

### Inline Queries - answer direct queries to bot
You must include  ```source modules/inline.sh``` in 'commands.sh' to have the following functions availible.

Inline Queries allows users to interact with your bot directly without sending extra commands.
As an answer to an inline query you can send back one or more results to the Telegram client. 
The Telegram client will then show the results to the user and let him select one.

##### answer_inline_query
answer_inline_query is provided for backward compatibility with older versions of bashbot.
It send back only one response to an inline query.

*usage:* answer_inline_query "$i{QUERY[ID]}" "type" "type arg 1" ... "type arg n" 

*example:* - see [Advanced Usage](3_advanced.md#Inline-queries)


##### answer_inline_multi
anser_inline_multi allows you to send back a list of responses. responses must be seperated by ','.

*usage:* answer_inline_multi "${iQUERY[ID]}" "res, res, ... res" 

*example:*
```bash
# note the starting " and ending " !!
answer_inline_multi "${iQUERY[ID]}" "
    $(inline_query_compose "1" "photo" "https://avatars0.githubusercontent.com/u/13046303") ,
    ...
    $(inline_query_compose "n" "photo" "https://avatars1.githubusercontent.com/u/4593242")
    "
```

#### inline_query_compose
inline_query_compose composes one response element to to send back. 

*usage:*  inline_query_compose ID type args ....

```
	ID = unique ID for this response, 1-64 byte long
	type = type of answer, e.g. article, photo, video, location ...
	args = mandatory arguments in the order they are described in telegram documentation
```

Currently the following types and arguments are implemented (optional arguments in parenthesis)
```
	"article"|"message"	title message (markup description)

	"photo"			photo_URL (thumb_URL title description caption)
	"gif"			photo_URL (thumb_URL title caption)
	"mpeg4_gif"		mpeg_URL (thumb_URL title caption)
	"video"			video_URL mime_type thumb_URL title (caption)
	"audio"			audio_URL title (caption)
	"voice"			voice_URL title (caption)
	"document"		title document_URL mime_type (caption description)

	"location"		latitude longitude title
	"venue"			latitude longitude title (adress foursquare)
	"contact"		phone first (last thumb)

	"cached_photo"		file (title description caption)
	"cached_gif"		file (title caption)
	"cached_mpeg4_gif"	file (title caption)
	"cached_sticker"	file 
	"cached_document"	title file (description caption)
	"cached_video"		file title (description caption)
	"cached_voice"		file title (caption)
	"cached_audio"		file title (caption)
```
see [InlineQueryResult for more information](https://core.telegram.org/bots/api#inlinequeryresult) about response types and their arguments.

----


### Background and Interactive jobs
You must include  ```source modules/background.sh``` in 'commands.sh' to have the following functions availible.

##### startproc
```startproc``` starts a script, the output of the script is sent to the user or chat, user input will be sent back to the script. see [Advanced Usage](3_advanced.md#Interactive-Chats)

*usage:* startproc "script"

*example:* 
```bash
startproc 'examples/calc.sh'
```

##### checkproc
Return true (0) if an interactive script is running in the chat. 

*usage:* checkprog

*example:* 
```bash
checkproc 
if [ "$res" -gt 0 ] ; then
  startproc "examples/calc.sh"
else
   send_normal_message "${CHAT[ID]}" "Calc already running ..."
fi
```

##### killproc
Kill the interactive script running in the chat

*usage:* killproc

*example:* 
```bash
checkprog
if [ "$res" -eq 0 ]; then
  killproc && send_message "${CHAT[ID]}" "Command canceled."
else
  send_message "${CHAT[ID]}" "Command is not running."
fi
```

----

##### background
Starts a script as a background job and attaches a jobname to it. All output from a background job is sent to the associated chat.

In contrast to interactive chats, background jobs do not recieve user input and can run forever. In addition you can suspend and restart running jobs, e.g. after reboot.

*usage:* background "script" "jobname"

*example:* 
```bash
background "examples/notify.sh" "notify"
```

##### checkback
Return true (0) if an background job is active in the given chat. 

*usage:*  checkback "jobname"

*example:* 
```bash
checkback "notify"
if [ "$res" -gt 0 ] ; then
  send_normal_message "${CHAT[ID]}" "Start notify"
  background "examples/notify.sh" "notify"
else
 send_normal_message "${CHAT[ID]}" "Process notify already running."
fi
```

##### killback
*usage:* killback "jobname"

*example:* 
```bash
checkback "notify"
if [ "$res" -eq 0 ] ; then
  send_normal_message "${CHAT[ID]}" "Kill notify"
  killback "notify"
else
  send_normal_message "${CHAT[ID]}" "Process notify not run."
fi
```

----

##### send_message
```send_message``` sends any type of message to the given chat. Type of output is steered by keywords within the message. 

The main use case for send_message is to process the output of interactive chats and background jobs. **For regular Bot commands I recommend using of the dedicated send_xxx_message() functions from above.**

*usage:* send_message "${CHAT[ID]}" "message"

*example:* - see [Usage](2_usage.md#send_message) and [Advanced Usage](3_advanced.md#Interactive-Chats)

----

### Aliases - shortcuts for often used funtions 
You must include  ```source modules/aliases.sh``` in 'commands.sh' to have the following functions availible.

##### _is_botadmin

*usage:* _is_botadmin

*alias for:* user_is_botadmin "${USER[ID]}"

##### _is_admin

*usage:* _is_admin

*alias for:* user_is_admin "${CHAT[ID]}" "${USER[ID]}"

##### _is_allowed

*usage:* _is_allowed "what"

*alias for:* user_is_allowed "${USER[ID]}" "what" "${CHAT[ID]}"

----

##### _kick_user

*usage:* _kick_user "${USER[ID]}"

*alias for:* kick_chat_member "${CHAT[ID]}" "${USER[ID]}"

##### _unban

*usage:* _unban "${USER[ID]}"

*alias for:*  unban_chat_member "${CHAT[ID]}" "${USER[ID]}"

##### _leave

*usage:* _leave 

*alias for:* leave_chat "${CHAT[ID]}"

----

##### _message

*usage:* _message "message"

*alias for:* send_normal_message "${CHAT[ID]}" "message"

##### _normal_message

*usage:* _normal_message "message"

*alias for:* send_normal_message "${CHAT[ID]}" "message"

##### _html_message

*usage:* _html_message "message"

*alias for:* send_html_message "${CHAT[ID]}" "message"

##### _markdown_message

*usage:* _markdown_message "message"

*alias for:* send_markdown_message "${CHAT[ID]}" "message"

----

#### _inline_button
*usage:* _inline_button "${1}" "${2}" 

*alias for:* send_inline_button "${CHAT[ID]}" "" "${1}" "${2}" 

#### _inline_keyboard
*usage:* _inline_keyboard "${1}"

*alias for:* _inline_keyboard "${CHAT[ID]}" "" "${1}"

#### _keyboard_numpad
*usage:* _keyboard_numpad

*alias for:* send_keyboard "${CHAT[ID]}" "" '["1","2","3"],["4","5","6"],["7","8","9"],["-","0","."]' "yes"

#### _keyboard_yesno
*usage:* _keyboard_yesno

*alias for:* send_keyboard '["yes","no"]'

#### _del_keyboard
*usage:* _del_keyboard 

*alias for:* remove_keyboard "${CHAT[ID]}" ""



### Helper functions

##### _is_function
Returns true if the given function exist, can be used to check if a module is loaded.

*usage* _is_function function

*example:* 
```bash
_is_function "background" && _message "you can run background jobs!"
```

----

### Bashbot internal functions
These functions are for internal use only and must not used in your bot commands.

##### get_file
*usage:* url="$(get_file "${CHAT[ID]}" "message")"

----

##### send_text
*usage:* send_text "${CHAT[ID]}" "message"

----

##### JsonDecode
Outputs decoded string to STDOUT

*usage:* JsonDecode "string"

##### JsonGetString
Reads JSON fro STDIN and Outputs found String to STDOUT

*usage:*  JsonGetString `"path","to","string"`

##### JsonGetValue
Reads JSON fro STDIN and Outputs found Value to STDOUT

*usage:*  JsonGetValue `"path","to","value"`

----

##### get_chat_member_status
*usage:* get_chat_member_status "${CHAT[ID]}" "${USER[ID]}"

this may get an official function ...

----

##### process_client
Every Message sent to your Bot is processd by this function. It parse the send JSON and assign the found Values to bash variables.

##### process_updates
If new updates are availible, this functions gets the JSON from Telegram and dispatch it.

----
##### getBotName
The name of your bot is availible as bash variable "$ME", there is no need to call this function if Bot is running.

*usage:* ME="$(getBotNiname)"

##### inproc
Send Input from Telegram to waiting Interactive Chat.

#### [Prev Best Practice](5_practice.md)
#### [Next Notes for Developers](7_develop.md)

#### $$VERSION$$ v0.76-1-ge8a1fd0

