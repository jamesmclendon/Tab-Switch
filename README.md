# Tab Switch
An AppleScript to send the frontmost tab from Chrome to Safari, or Safari to Chrome.

```applescript
tell application "System Events"
	set theBrowser to name of the first process whose frontmost is true
end tell

if theBrowser is not "Safari" and theBrowser is not "Google Chrome" then
	display dialog "Send which tab where?" buttons {"Safari → Chrome", "Chrome → Safari", "Cancel"} default button 1
	if result = {button returned:"Safari → Chrome"} then
		set theBrowser to "Safari"
	else if result = {button returned:"Chrome → Safari"} then
		set theBrowser to "Google Chrome"
	end if
end if

if theBrowser is "Safari" then
	tell application "Safari"
		set theURL to URL of current tab of window 1
		close current tab of window 1
	end tell
	tell application "Google Chrome"
		open location theURL
		activate
	end tell
else if theBrowser is "Google Chrome" then
	tell application "Google Chrome"
		set theURL to URL of active tab of first window
		close active tab of first window
	end tell
	tell application "Safari"
		open location theURL
		activate
	end tell
end if
```
