# Audio-webui.pinokio

One click installer for https://github.com/gitmylo/audio-webui

# Explanation

## install.json

The install script

```json
{
  "run": [{
    "method": "shell.run",
    "params": {
      "message": "git clone https://github.com/gitmylo/audio-webui"
    }
  }, {
    "method": "shell.start",
    "params": {
      "path": "audio-webui"
    }
  }, {
    "method": "shell.enter",
    "params": {
      "message": "{{os.platform() === 'win32' ? 'python main.py' : 'bash install.sh'}}",
      "on": [{
        "event": "/Press any key to exit/",
        "return": true
      }]
    }

  }, {
    "method": "notify",
    "params": {
      "html": "<b>Install complete!</b> Click to go to the start script.",
      "href": "start.json"
    }
  }]
}
```

1. The first step runs `shell.run` to clone the audio-webui repository https://github.com/gitmylo/audio-webui
2. The second one starts a persistent shell session with the default execution path of "audio-webui" (which is where the github repository is downloaded by default)
3. The third script runs the install script. In case of windows it runs `python main.py`, and for the rest it runs `bash install.sh`
4. The third `shell.enter` method also waits for a pattern in the terminal that matches `/Press any key to exit/` (regular expression), and when it does, it returns, moving on to the next step.
5. Finally it displays the notification popup with `notify`, which when clicked, sends you to the start script at [start.json](start.json)
