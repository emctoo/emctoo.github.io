## [Embed the Google Assistant (Python)](https://developers.google.com/assistant/sdk/guides/service/python/embed/setup)

```shell
sudo apt install alsa-utils
# check mic: card:device
arecord -l
# check speaker card:device
aplay -l
```

```shell

```

$HOME/.asourndrc，其中 `pcm "hw:<card>,<device>"`

```
pcm.!default {
  type asym
  capture.pcm "mic"
  playback.pcm "speaker"
}

pcm.mic {
  type plug
  slave {
    pcm "hw:1,0"
  }
}
pcm.speaker {
  type plug
  slave {
    pcm "hw:1,0"
  }
}
```

```shell
alsamixer
speader-test -t wav
arecord --format=S16_LE --duration=5 --rate=16000 --file-type=raw out.raw
aplay --format=S16_LE --rate=16000 out.raw
```

创建一个venv

```sh
sudo apt-get install portaudio19-dev libffi-dev libssl-dev

pip install -U google-assistant-sdk[samples] google-auth-oauthlib[tool]
google-oauthlib-tool --scope https://www.googleapis.com/auth/assistant-sdk-prototype \
      --save --headless --client-secrets /path/to/client_secret_client-id.json
googlesamples-assistant-pushtotalk --project-id my-dev-project --device-model-id my-model
```

google-oauthlib-tool 会提示授权并得到一个code，复制粘贴到 prompt。最后会生成 `~/.config/google-oauthlib-tool/credentials.json` 文件 (For Windows, it's `C:\Users\xiaogang.huang\AppData\Roaming\google-oauthlib-tool\credentials.json`)

### Will [proxify](https://github.com/projectdiscovery/proxify) help on this?