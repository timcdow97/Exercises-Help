Create Master Socket to Jump / Gray Host
ssh -MS /tmp/gray student@10.50.#.#
Cancel Master Socket to Jump / Gray Host
ssh -MS /tmp/gray -O cancel student@10.50.#.#
Port Forward
Create Port forward through Master Socket to Next Hop/host
ssh -S /tmp/gray dummy -O forward -L 1330:192.168.28.#:80
Cancel Port forward through Master Socket to Next Hop/host
ssh -S /tmp/gray dummy -O cancel -L 1330:192.168.28.#:80 
Dynamic Forwarding
Create Port forward through Master Socket to Next Hop/host
ssh -S /tmp/gray dummy -O forward -D9050
Cancel Dynamic Tunnell
ssh -S /tmp/gray dummy -O cancel -D9050 (Cancel Dynamic tunnel)
