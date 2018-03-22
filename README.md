# nginx-slim

A slim Docker image for NGINX.

## Docker Images

To build a Docker image of NGINX 1.13.1 (≅4.32MB), run

```
$ docker build --tag <repo>:<tag> mainline/
```

To build a Docker image of NGINX 1.12.2 (≅4.27MB) run

```
$ docker build --tag <repo>:<tag> stable/
```

## Binaries

To grab pre-built static binaries head over to the
[releases](https://github.com/bmcstdio/nginx-slim/releases) page. Alternatively,
run

```
$ docker create bmcstdio/nginx-slim:1.13.10-0
3f5f24dff033baca166b60ee0f32c45a12edfd8ed07155a46e85d045a7d51208
$ docker cp 3f5f24d:/nginx nginx-linux-amd64
```

or

```
$ docker create bmcstdio/nginx-slim:1.12.2-0
0d650281cefad185ba78dbd839855d1b02ee45002d22241b15713866e7ba6844
$ docker cp 0d65028:/nginx nginx-linux-amd64
```

to copy the required binaries to your current working directory.

## License

Copyright 2018 bmcstdio

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
