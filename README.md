# flow

The flow module simplifies asynchronous flows of execution where your
code needs to wait for one asynchronous operation to finish before
starting with the next one.

```lua
local flow = require "flow.flow"

function init(self)
	flow.start(function()
		-- animate a gameobject and wait for animation to complete
		flow.go_animate(".", "position.y", go.PLAYBACK_ONCE_FORWARD, 0, go.EASING_INCUBIC, 2)
		-- wait for one and a half seconds
		flow.delay(1.5)
		-- wait until a function returns true
		flow.until_true(is_game_over)
		-- animate go again
		flow.go_animate(".", "position.y", go.PLAYBACK_ONCE_FORWARD, 400, go.EASING_INCUBIC, 2)
	end)
end

function final(self)
	flow.stop()
end

function on_message(self, message_id, message, sender)
	flow.on_message(message_id, message, sender)
end
```