# pps-patch
Plutus playground server fix for 30 seconds timeout during compiling and evalution.

This walkaround is actual only if you have to check out ea0ca4e9f9821a9dbfc5255fa0f42b6f2b3887c4 tag and still based on the hardcoded constant (wich I increased from 90 to 300 seconds).
At the current moment the issue fully fixed: https://github.com/input-output-hk/plutus/issues/3509

If you faced with such kind of error during compilation or evalutation exactly after 30 second after start

<i>ConnectionError (HttpExceptionRequest Request { host = "localhost" port = 8080 secure = False requestHeaders = [("Accept","application/json;charset=utf-8,application/json"),("Content-Type","application/json;charset=utf-8")] path = "/runghc" queryString = "" method = "POST" proxy = Nothing rawBody = False redirectCount = 10 responseTimeout = ResponseTimeoutDefault requestVersion = HTTP/1.1 } ResponseTimeout)</i>

you need to replace file in directory <b>plutus/plutus-playground-server/src/Playground/Server.hs</b> with the given file in this repository.
Then go to the plutus root directory and run following command (you have to be in nex-shell!):

nix build -f default.nix plutus.haskell.packages.plutus-playground-server.components.exes.plutus-playground-server

after succesful building start server as usual.

If you face with the 'out of space' error during nix build, run this command

mkdir ~/tmpdir; export TMPDIR="$HOME/tmpdir" and run build again.
