# Processes and Jobs
## 1. Listing Processes
```
hacker@processes~listing-processes:~$ ps -efww
UID          PID    PPID  C STIME TTY          TIME CMD
root           1       0  0 21:08 ?        00:00:00 /sbin/docker-init -- /nix/var/nix/profiles/dojo-workspace/bin/dojo-init /run/dojo/bin/sleep 6h
root           7       1  0 21:08 ?        00:00:00 /run/dojo/bin/sleep 6h
root         133       1  0 21:08 ?        00:00:00 /challenge/9914-run-3998
root         136     133  0 21:08 ?        00:00:00 sleep 6h
hacker       147       1  0 21:08 ?        00:00:00 /nix/store/g0q8n7xfjp7znj41hcgrq893a9m0i474-ttyd-1.7.7/bin/ttyd --port 7681 --interface 0.0.0.0 --writable -t disableLeaveAlert true /run/dojo/bin/bash --login
hacker       149     147  0 21:09 pts/0    00:00:00 /run/dojo/bin/bash --login
hacker       159     149  0 21:09 pts/0    00:00:00 ps -efww
hacker@processes~listing-processes:~$ ps -efww | grep challenge
root         133       1  0 21:08 ?        00:00:00 /challenge/9914-run-3998
hacker       161     149  0 21:09 pts/0    00:00:00 grep --color=auto challenge
hacker@processes~listing-processes:~$ /challenge/9914-run-3998
Yahaha, you found me! Here is your flag:
pwn.college{AGs6TZcEZjOhfEXf8tEJurrX0OD.QX4MDO0wSMwEzNzEzW}
Now I will sleep for a while (so that you could find me with 'ps').
```
### Steps

I inspected the system to see which processes were running in the environment. I listed all processes with wide output to capture full command lines and then filtered the results to locate any process whose name related to the challenge. Once I found the target process, I invoked it directly to reveal the flag.

### What I Learned

I learned how to enumerate processes and interpret columns such as PID, PPID, user, start time, and the full command. I also practiced filtering process listings to quickly find a particular service or binary. This taught me how process discovery can be used to locate sleeping or backgrounded challenge programs.

### References

man ps
## 2. Killing processes
```
hacker@processes~killing-processes:~$ ps -efww | grep dont_run
hacker       136     135  0 21:15 ?        00:00:00 /challenge/dont_run
hacker       163     152  0 21:15 pts/0    00:00:00 grep --color=auto dont_run
hacker@processes~killing-processes:~$ kill 136
hacker@processes~killing-processes:~$ ps -efww | grep dont_run
hacker       166     152  0 21:15 pts/0    00:00:00 grep --color=auto dont_run
hacker@processes~killing-processes:~$ /challenge/run
Great job! Here is your payment:
pwn.college{4yxj2skHhC59tKt3A5BpNI8ebDu.QXyQDO0wSMwEzNzEzW}
hacker@processes~killing-processes:~$ 
```
### Steps

I looked for the misbehaving process by scanning the process list for a recognizable name. After confirming its PID, I sent a termination signal to that PID to stop the process. I then rechecked the process list to ensure it was gone, and proceeded to run the challenge to receive the reward.

### What I Learned

I learned how to find and terminate processes by PID, and confirmed that killing a process frees up whatever resource or lock it held. I also learned to re-verify the process list after termination to ensure the action succeeded. This reinforced safe, targeted process termination practices.

### References

man kill

man ps — process identification and verification
## 3. Interrupting processes
```
hacker@processes~interrupting-processes:~$ /challenge/run
I could give you the flag... but I won't, until this process exits. Remember, 
you can force me to exit with Ctrl-C. Try it now!
^C
Good job! You have used Ctrl-C to interrupt this process! Here is your flag:
pwn.college{MhSVCUpR1fkdUnqxyFAjP71-dUN.QXzQDO0wSMwEzNzEzW}
hacker@processes~interrupting-processes:~$ 
```
### Steps

I ran the interactive challenge process and observed that it would not give the flag until the process exited. I used a keyboard interrupt to send the process an interrupt signal, which caused it to stop immediately and output the flag.

### What I Learned

I learned that a keyboard interrupt (SIGINT) forces an interactive program to stop and that many programs use this behavior intentionally as a puzzle mechanism. I also learned when it’s appropriate to use an interrupt instead of gracefully terminating a process.

### References
none
## 4. Misbehaving processes
```
hacker@processes~killing-misbehaving-processes:~$ ps -efww | grep decoy
root         139       1  0 11:54 ?        00:00:00 su -c exec /challenge/decoy > /tmp/flag_fifo hacker
hacker       142     139  0 11:54 ?        00:00:00 /usr/bin/python /challenge/decoy
hacker       168     157  0 11:56 pts/0    00:00:00 grep --color=auto decoy
hacker@processes~killing-misbehaving-processes:~$ kill 142
hacker@processes~killing-misbehaving-processes:~$ kill 139
bash: kill: (139) - No such process
hacker@processes~killing-misbehaving-processes:~$ /challenge/run
Sending the flag to /tmp/flag_fifo!
cat /tmp/flag_fifo

^C
hacker@processes~killing-misbehaving-processes:~$ cat /tmp/flag_fifo &
/challenge/run
[1] 173
pwn.college{Q6OOz-4hS6VPM4T6HwMLXYfwLtMD.U79g8ClXl8L1MmHC2C}
pwn.college{j6eMKjyPShbDT52grMD7UrafIwLzvQsoTvbhPDc5NvxxOyl}
pwn.college{-kr.FwLKhDsy3dibNCUfV1rJ66coNd6xEcs23sXaqIDflC0}
pwn.college{TFxOeSLsCLMmLW44X.IlDwIJxejdDwBBMJl-ZQTwrXe96Ce}
pwn.college{hGjKKaPvzf10kWeK2RoRhuNes3PCA-57Z-4NlnzDDBzJNe1}
pwn.college{tnSXlrZ-98gy-aSY.5MgMBHlt5nqMYnfEr8ZlOGkZPbALKt}
pwn.college{2lqYxGSxOPBLhQC2zHT8CywUp38NDpwMPM4KwDGdV.VeKlI}
pwn.college{fBGAFIEtCdJiygUlnuPEVLa9E81Ymy75XP3dXt1WWvd4dnj}
pwn.college{oYsNtoi4iZNq9cfQHYCN.XtDyQcaS5zScVch9UlW0f.XXme}
pwn.college{KT7k2Hl6yFZpZ9zGLAmP9uSlZ7EZ9yO5qpJGlBXWLjqHS6K}
pwn.college{IvxXhOmOq0ORCO21E5FIKVcuHcc6rl0gntpzUug1WN5FwEh}
pwn.college{LjPxKLGX4bss36np-odnIw8qoeQelnicMqX0XoUciVCy.A0}
pwn.college{ZkB8LEoHi1HbH2Yfj6NPREwuXKwCAGja3go7uL1jtWxa77F}
pwn.college{jUDWxOCXp5s-I3XB2koMHfFG-uN9VaDQyDd4VdGjZZBC2ql}
pwn.college{w-2WlBsDMCQXFAkB-dmskzgdOXyG5aGyr9jMYr425eIUk4o}
pwn.college{rYq5Dr0AwOgPUguFpd.OqxawW7KdzpTZlD29eLDhWfKDYGF}
pwn.college{Bxqm9pg-0Lo-g0FhFXc7InWhudh7jPHFRQWmxfGd.pb44dn}
pwn.college{y7C6SltFioWJ.cRucr-Zl2WhkOXN2zEJIb-4U0iuoM3med6}
pwn.college{ThpVOSe5zk79uRaQ409HWZqQU5x48AOa2pHh1RfW3DU9eCY}
pwn.college{lTr2jlnFNlb3AaokviZwRr5DQ6Ycudr0z9MC9zlF7wTiKER}
pwn.college{c8p9LSXmW5nMU4Oyg6CyKWQ5lD41NqIvvHQ7N6EgZmqwVmw}
pwn.college{kEUKOnVOTp9tM1MUrvRMRc4yEdImu1uHf2j-OmYKfjBi2dy}
pwn.college{IEwRNiuOMeiA.KvuFyclE8P8E4zRbOxg.ohCsKqQs6T2tLw}
pwn.college{T3skNnslt40CCQKNJAojOkRmlVBWRfDGPq-4ede5CveLjat}
pwn.college{1aa4-GRfOcX00VjmVetkZfs8O2oo88fp6xvnWjzUvrIL8hg}
pwn.college{vsndu68t98p3OfLPJRWsWtoFVSrGo7Q0N3nbZ848zvoammy}
pwn.college{3u9HBgj20NhW0OAWzV8eriqRgRKKy8fXvbQp4Ir0XZQc2Pn}
pwn.college{qzt1fGw9npoDWotH8TzFMgc.ievAWUvx--.Q6oE96o4hcmy}
pwn.college{W3qsqEC.J-nl4wxn0WDphm3SUiYXItX.-dxZOBrg5jCgz.s}
pwn.college{GEYuro5HX6bVUPWAlU9Q7XEtBpEEh-oS0NHGQQeQ5KiSgoB}
pwn.college{K0Hdcf4-zAntLVBRhVK665S88vsUWgfX2uWl.lcl3SZW-TB}
pwn.college{kikfznhf1Lv9OQ3wDYO2zMaib9nC9UDsm7TB9NZPUip2rLx}
pwn.college{bOjIOyjpROKvvvFmNG2RfEm9X6QMziRyi6FICvoxwAwnxwE}
pwn.college{uxnYrsjw9Ra3bVk5Ipq4WfpvRj4OCey27nyetu-DIzWkJOF}
pwn.college{QKbx9sGT.PcJiLX9ZpXkKOJuo0.EPnEMD3DOuxf1e5-QGVG}
pwn.college{DHLDRxAKG0x6wACRdEutKbyS1YNgjmNRy6wUw8.OJoxGU2e}
pwn.college{wkEpldm.VhJ0Gvjik139aJpv6aAwjvL8ax2GEoi.IYXNcHU}
pwn.college{vEOf1o0mZSd8.987Ny0qzHxGcIdArBmTYpJTGZhmy2Z1eV6}
pwn.college{WbJwDUA-BuldUYyuwy9kT1F-dqB1UgeMikx1ZCga9vff.1.}
pwn.college{Xr5PnBqo8VEblxPG5jt1vcYQ9PvIS2TI1gza97n8ayPNQha}
pwn.college{cLaGkhv2pK.esEzNLcfOqivrVD7oi5HGeSESX9kHlDfDbOj}
pwn.college{sbWBXGbR3bhixDrkmxBwrb7aqkKpCvkKaUU.t00DelD04vw}
pwn.college{k-tRRq4Qp7x39shL8FvHe83jj.FcacfS7goTrhxswfB6Q2X}
pwn.college{FnYYs6bILzGUjTfic8v-wKUzmfB8E6adeE444qEio3BCrDY}
pwn.college{.KwfuuPeycMf5x2OMdd8GsYACKzeUA5qxAGlzgIo2fB9LDu}
pwn.college{lF7MdTYznu0KTZcOVLMVCfzurIbtUd4RJDAmev0P.7i3RX9}
pwn.college{HlJyZtes2sMj5iAE18sNYFBMWRQv5h.KcomOVQMMITsGYwm}
pwn.college{XSZnkRvLID.0tlJeIVOaDKSSK7sKJlOvgqtOG1QA.wBLBqg}
pwn.college{oY3UeN93ciUyJJMSEfjCsc7TAdXJDgp3ExEaL4HypTGtfi4}
pwn.college{QlkKSaMCice2ZBYhluqWH5FaHnbb1i85rRmrCOASIjBp8Qy}
pwn.college{S6tClS2H7OBbHwVS60BDJAziKpky5-cGG5rJUViiXoknwOt}
pwn.college{kOGgwGAqZR7ZFMMrgTG5oBki8HDdEKQo9UuQ3-NhACDWoSS}
pwn.college{WfqLQkbeimMzC3T9X4f3GR5tfSh1YRPG3W701afGuRpkS7X}
pwn.college{2M6YtF0TniE9bHH0OzD.sAW5KGUFa1Lpohq1WzUDkDhtKJ1}
pwn.college{YzhAsbHByT3Lcq.SwYrt.biBSFk2mBq28CH0.cnZGHzY9UO}
pwn.college{qN3syETzgpsdn57cD-hsVAEM0Txh5Gq-1-EnEloINJbUbyj}
pwn.college{qzoSliVsRfWSx-.9hrnDmv0sHFG9Y4YXRiicAFB4tkdIPKu}
pwn.college{x3m62ZXM1wTA8VHKFBSi5tRcxj4BzzhhjOyy00aS22jif.6}
pwn.college{QJqHKVkmuKUG.WgZCr1F9EUZZOlx.RLUGyNadMLyzWauxv.}
pwn.college{ScCTQgtZQRYYf7BQn6YLVGvw55ydP5BASz8aSt7cw5p0PFw}
pwn.college{WGtStGXj87APVhgViN6Zv.bvaF.O0uztIiTp5s9HSN2pjUk}
pwn.college{bAN5jrWJCJFDc5TsYFA58eU5Vh2ZE4syPYNWMSteGPafOTx}
pwn.college{.ZZ7LrjOma1dCVwU1lmbxU6bHZux97YEGF8gYsKUcknwS0k}
pwn.college{MCleWMGyy1nEMU6KWrfXbi82D1CgneRZHDRtcp19QsZYvzd}
pwn.college{i4hUhI4tiBX5ciO8.7uUpmy9dEVwwnJIvTvvuyt7in0Pw0-}
pwn.college{E.En7rN0RSs4UconOzPoDByfyinlS3fnJeQNaxDDXfISCDY}
pwn.college{lMg2TjPqVB3eTCcLTLseNT6afryAgmXIdeC2vuBqmOPiwrb}
pwn.college{u9hkDriYSWKi3o6uaPc9XzapjiXRNxTvnEMOlocUxVRd2Ej}
pwn.college{82jHH3X0uI2aXAnVy7CkMB4w5dE1WMzD0zLHDazOAWT.DRU}
pwn.college{hnBWuUnHsFRolqzNTBwPU4jhPMkF5-RiL2ekX5N3bayJX12}
pwn.college{5SE8Ez23xtCX-CfnRS8FwrLHdiVy3Y0EsoH8Ar2a8u9WGnF}
pwn.college{tfwLdHT8X5wRucx.1qCv5Abndhaggiv5IjIwPNcQJPDBbGZ}
pwn.college{BPdcWCLcXh4Rc5h3ALY1.wkbswlhASDbsuQebFG89SyLpBV}
pwn.college{FUydRPFf1G3qoQcCfbZKm2u.KOCQJMHjj654NCgEkqMEh0H}
pwn.college{VmHx-n2Ekoo7ScaxupHT2Ez6ELiHWM5zV3VfmdxnDeWFILR}
pwn.college{p7dz3iXSt5-gRHs3jTF9wG-ezCFlL8cxRBi0JkAJRbHHH-O}
pwn.college{3Zhj5Yf2y9s.nSjqEoM53tclW2pc1U32htqow4ABA3p9pKF}
pwn.college{iJYx8cOkb6XdBWAert.O76ISMqjkRfIbXw8PLfvoKmYrdz.}
pwn.college{DQrYa6O.wblAZv4Pu1YhOJrYnDFrfgp-0pgCUMTdr1dPQrb}
pwn.college{rhSgOx5TRrYdVKKp3sQ3erlyAkhnH5cvKdJpq5O1zQBTjsN}
pwn.college{RpgOlsGV4ociaAKSLmwOZ4nAbZsmoNlz7KGrEEJp4NAa9oO}
pwn.college{nAbHSGIIqKERXGUdiXtAzaYTM6FJxbFHAGmrmkFY5THV7qm}
pwn.college{CS6no6Vu23Dnkij18NTKv34na2Fcdj-n49UUoUVo4SRShHl}
pwn.college{BQrmNRxdamyNMwI0c6z7oGCnycx5g6LcFjBIDprkSqzAgjQ}
pwn.college{JnZUOuqIyoOb7c6wECvNvpg9uBLX3PCH8jmaYkBroRNNc8o}
pwn.college{moONN2ZD-v0YeBNES2z9DjEB-xOKoExiIZHnAXzoyGob36R}
pwn.college{3iihE30RUviTjFLmE18XOlt0toB-uhj0JJwma5Z0NCT1H8o}
pwn.college{wT1b7mKYDrok0.2-8BItJyPhsH3gQZefUY60hPfgaOetOon}
pwn.college{vUZV9iPzp8M4npKyzYV6LS2cURKFaJxSlH.6QhGU-T3iw61}
pwn.college{j9pBJIApUOo5lWNhjAXXXCehF-CAJpMbzh1TUem8oy1E3wY}
pwn.college{Eii8N0H7lEbOKfCRqCpJfPRkI2Ll0ezjbTWwTpbVs9AOSCQ}
pwn.college{IhAT.XTngkXy.JAzM1e6ONymZhjvGhXqi6egbV4u6mzIZ87}
pwn.college{sBfVJtJAwGiGjTdqlzNAn5dmuOiLLAq26Wc2hmE3VIkCwN5}
pwn.college{A8puphz-wd7qXpTgitBmj0wY7yvoDwEmyqiiG47DSWKsMYy}
pwn.college{jBN3bnGj22ldYulMGlg2wiuOqAYc9wA-SKlUj2f5toLkCDO}
pwn.college{6O4H-lQsNlzkVLoYJNmNlOGFdieAAr4sK3mySDFzLh0s0ff}
pwn.college{JW9e55pWq.Ey.iuIApAU7SCPLidiSZjO3YQjrgIeG5e7RzC}
pwn.college{xdiyj47-V7KD24kV6sFID2k2JNLWUkaZnMjCyb1v7UvhzwI}
pwn.college{AjSeut1Zs5tQpQri-McAlZho3OOPZQScDVLJ-zaTnJZpAad}
pwn.college{fb0KPfEWxRlqghiGLNbXHX1gCkQGB6VfYkryIRZYQiL5UOu}
pwn.college{JTZFj8raKdXbriDQX94EQXCsDoPBAO9aUvmgiEJLGPtGRTD}
pwn.college{UpujhUXfyuMmW8g7Tc-4BLJ8T2kqu963h51dHQPpegRSR9D}
pwn.college{IrxU2aGMtKy7whl7vSIBnjADmGvm-LbxQ-NPb8hDlJl925q}
pwn.college{JL.yPwau1JA1F5ovuYBRODHMONg759HdJuR-8HkGD.eptWC}
pwn.college{pL2Jx9nGISypnQbPuq5JNl37Opqmg3Zcj32myXaAvrq8-vo}
pwn.college{kj-BZfiC4dEFJwjYP1H1T3vrvIZQy1ROBr0WVbMpqft52T0}
pwn.college{p0kW3DyK4dEoruiDH08N.djq21mD.OBMDFR5MJf6FG1LVwQ}
pwn.college{mPuL-U.33IyscQC8imR-AAPWde9HCP0mrstGxWV6snd4C.2}
pwn.college{1oqAq35IixqK224tzygeJT0NqgiD0ybxYZuO.I2pU.Nv6lO}
pwn.college{djFEuOMNbRIvz-7gmXdeFc6E4Ldh4vtmlriIrj8rDV10u6t}
pwn.college{Fx50s4AMBfSrlUPod3HnpG11KQf4sUD.25qFqCmyA8ACytc}
pwn.college{e2RD-ugNHM.BOdt7anV8qISo6UmBtaxbqj3Z1TpQIEzlSnh}
pwn.college{orh7MC8DBCq8iHRDvJUdz1drHZPwXC9E33cOy-VxAyuiU--}
pwn.college{7a-OixKIwUeuQbd5DtwR10bvjS70q0GhY0TYekX-206n6-1}
pwn.college{RtbknVBM3X09dsmKsIcLHO1omnxTpyM.rcx7Ib.gQDdEKgP}
pwn.college{cfzG16Gq0ftTMrnnGhbJFRaeAL9bMpf4oJi6e5j7W47TVVA}
pwn.college{goiHVuDEeEfI76TYfyRCT7tTIGX48dJYTk6HFMeueZzxj5X}
pwn.college{LDe27l9P0S9nfuwFcO9SNdNBfUQHu0078CHbxOUrlt9Ab72}
pwn.college{ojQ1raciJNSCiQGOFSthN2sUhylYTZ9dP4UOIG8GNbP4Dho}
pwn.college{Rggyb2sia5qkLmD.QuwcH5.40znvveGGOoa73cCfadS-iby}
pwn.college{e-8uaR0ZfnEoFcCUkRfOh4ml06KxjzBBAvpfc73NZtUQy29}
pwn.college{yhnUBSkJ65ijUfWz3eTwgBRlazQHTgKpaXefsNl8uyq6oVO}
pwn.college{vm4w6jf2GIF6GRQmPTxH1ZD93cytOUPOEj0J4Wr-r8PixTP}
pwn.college{PbHGP4tiftZwpsbatKDK.MNR78nOYz4dCCyXfDoPeSCGlwg}
pwn.college{c8Vj.3Rigq-fWYxqPVMUqIFa3w9V2bx8yRTj-uDFNy9kVal}
pwn.college{K2sC6QXv1wuQtFnEhhANaB5PAAcgst8DWfuPWYO9Oht84ON}
pwn.college{a5UB8rtHcLHtji2rDhk.vGI3zzCGFO5uR4ww7S4GN7h9JgK}
pwn.college{9A4egiU62z4OhcFCeBYthKfs2VpKVtmGpWgczUVPQ0zeOBx}
pwn.college{8sKa80JhRfyDCz78S4itedSpbJmc-h-Dl6EzXq7UR4AAn.G}
pwn.college{mfbzNyxopQxJrWrm-y4hYcyFX6MC2WajOx3ib.Pp-nJL-Bx}
pwn.college{kKud9vqu28CiX3QYXLcuC4UgPnBa6G0fMX5kx0Pvkel84eF}
pwn.college{SfXywSLXxmRNI05WZSKSbulrM4Rgy81ZItO5pxBILq9q-H-}
pwn.college{SG.t108qE4rvmONYvt5wMUT7Ri9Ks6RYpkk8stICNmuvLV7}
pwn.college{lRcXSBdnzTfv7SFKxv8lWvY6Ukx15mQgar01lZzSAhhQJSF}
Sending the flag to /tmp/flag_fifo!
pwn.college{oaDIy7RQyC8N6UXDIukmH-aHb6Q.0FNzMDOxwSMwEzNzEzW}
hacker@processes~killing-misbehaving-processes:~$ 
```
### Steps

I inspected the process table and noticed a decoy process running under a different user context. I terminated the decoy process and any associated parent processes I could control. After that, I observed the program writing a flag into a named FIFO (a temporary file used as a pipe). I read from that FIFO (backgrounding the reader as needed) to capture the flag outputs being sent by the program.

### What I Learned

I learned how parent/child process relationships can affect control over services, and how some programs use IPC mechanisms (like FIFOs) to deliver outputs. I practiced terminating both direct child processes and supervising processes where possible, and I learned how to consume output asynchronously via backgrounded readers.

### References

Documentation on inter-process communication (FIFOs / named pipes)

man ps, man kill for process hierarchy and termination
## 5. Suspending processes
```
hacker@processes~suspending-processes:~$ /challenge/run
I'll only give you the flag if there's already another copy of me running in 
this terminal... Let's check!

UID          PID    PPID  C STIME TTY          TIME CMD
root         146     136  0 14:08 pts/0    00:00:00 bash /challenge/run
root         148     146  0 14:08 pts/0    00:00:00 ps -f

I don't see a second me!

To pass this level, you need to suspend me and launch me again! You can 
background me with Ctrl-Z or, if you're not ready to do that for whatever 
reason, just hit Enter and I'll exit!
^Z
[1]+  Stopped                 /challenge/run
hacker@processes~suspending-processes:~$ /challenge/run
I'll only give you the flag if there's already another copy of me running in 
this terminal... Let's check!

UID          PID    PPID  C STIME TTY          TIME CMD
root         146     136  0 14:08 pts/0    00:00:00 bash /challenge/run
root         153     136  0 14:09 pts/0    00:00:00 bash /challenge/run
root         155     153  0 14:09 pts/0    00:00:00 ps -f

Yay, I found another version of me! Here is the flag:
pwn.college{At0foM0y9BpUL6oizQqIOvBMwWP.QX1QDO0wSMwEzNzEzW}
hacker@processes~suspending-processes:~$ 

```
### Steps

I started the challenge program and discovered it required a second running copy to produce the flag. I suspended the running instance (sending it to the stopped state), launched a new instance, and confirmed the challenge detected the suspended-first-copy as an existing instance and produced the flag.

### What I Learned

I learned how suspending a process puts it into a stopped state while preserving its PID and context. I also learned how some programs check for other instances by inspecting the process table, and that intentionally suspending a process can be used to meet those checks without terminating the original instance.

### References

idk, i just solved it from the question
# 6. Resuming Processes
```
hacker@processes~resuming-processes:~$ /challenge/run
Let's practice resuming processes! Suspend me with Ctrl-Z, then resume me with 
the 'fg' command! Or just press Enter to quit me!
^Z
[1]+  Stopped                 /challenge/run
hacker@processes~resuming-processes:~$ fg
/challenge/run
I'm back! Here's your flag:
pwn.college{kzI0ARxWfXHwZNesXqg_vxoqTLA.QX2QDO0wSMwEzNzEzW}
Don't forget to press Enter to quit me!

Goodbye!
hacker@processes~resuming-processes:~$ 
```
### Steps

I followed the exercise by suspending the active challenge process and then bringing it back to the foreground. After resuming it, the program resumed execution from where it left off and produced the flag.

### What I Learned

I learned how resuming a stopped process restores it to running state in the foreground, preserving its standard input/output context. This highlighted the difference between stopped, backgrounded, and foreground states, and how resumption is used in interactive workflows.

### References
idk, i just solved it from the question
## 7. Backrounding processes
```
hacker@processes~backgrounding-processes:~$ /challenge/run
I'll only give you the flag if there's already another copy of me running *and 
not suspended* in this terminal... Let's check!

UID          PID STAT CMD
root         146 S+   bash /challenge/run
root         148 R+   ps -o user=UID,pid,stat,cmd

I don't see a second me!

To pass this level, you need to suspend me, resume the suspended process in the 
background, and then launch a new version of me! You can background me with 
Ctrl-Z (and resume me in the background with 'bg') or, if you're not ready to 
do that for whatever reason, just hit Enter and I'll exit!
^Z
[1]+  Stopped                 /challenge/run
hacker@processes~backgrounding-processes:~$ bg
[1]+ /challenge/run &
hacker@processes~backgrounding-processes:~$ 


Yay, I'm now running the background! Because of that, this text will probably 
overlap weirdly with the shell prompt. Don't panic; just hit Enter a few times 
to scroll this text out.

hacker@processes~backgrounding-processes:~$ 
hacker@processes~backgrounding-processes:~$ 
hacker@processes~backgrounding-processes:~$ /challenge/run
I'll only give you the flag if there's already another copy of me running *and 
not suspended* in this terminal... Let's check!

UID          PID STAT CMD
root         146 S    bash /challenge/run
root         156 S    sleep 6h
root         157 S+   bash /challenge/run
root         159 R+   ps -o user=UID,pid,stat,cmd

Yay, I found another version of me running in the background! Here is the flag:
pwn.college{YqzXJh468SujKmixCIq0GYiidnn.QX3QDO0wSMwEzNzEzW}
hacker@processes~backgrounding-processes:~$ 
```
### Steps

I suspended a running instance and then resumed that suspended instance in the background. After ensuring a background copy was active and not suspended, I launched a new foreground instance which verified the background process’s presence and returned the flag.

### What I Learned

I learned how to move processes to the background while leaving them running, how to check their status, and why some programs consider a background running instance as "another copy" for their checks. I also practiced managing potential output overlap between background jobs and the interactive shell.

### References

man ps for STAT column meaning
## 8. Foregrounding Processes
```
hacker@processes~foregrounding-processes:~$ /challenge/run
To pass this level, you need to suspend me, resume the suspended process in the 
background, and *then* foreground it without re-suspending it! You can 
background me with Ctrl-Z (and resume me in the background with 'bg') or, if 
you're not ready to do that for whatever reason, just hit Enter and I'll exit!
^Z
[1]+  Stopped                 /challenge/run
hacker@processes~foregrounding-processes:~$ bg
[1]+ /challenge/run &
hacker@processes~foregrounding-processes:~$ 


Yay, I'm now running the background! Because of that, this text will probably 
overlap weirdly with the shell prompt. Don't panic; just hit Enter a few times 
to scroll this text out. After that, resume me into the foreground with 'fg'; 
I'll wait.

hacker@processes~foregrounding-processes:~$ fg
/challenge/run
YES! Great job! I'm now running in the foreground. Hit Enter for your flag!

pwn.college{Ia56O70_GJtVJrGuvtviYcUlnWq.QX4QDO0wSMwEzNzEzW}
hacker@processes~foregrounding-processes:~$ 
```
8. Foregrounding Processes
### Steps

I suspended a running program, resumed it in the background, and then brought it back to the foreground without re-suspending it. The challenge required exactly that sequence, and once I foregrounded the background job the program acknowledged it and produced the flag.

### What I Learned

I learned the precise workflow for suspending, backgrounding, and foregrounding processes so that a program can be moved through states without losing execution context. This exercise clarified subtle timing and state requirements of interactive job control.

### References
again, i just solved it from the question and the examples
## 9. Starting backround processes
```
hacker@processes~starting-backgrounded-processes:~$ /challenge/run
You've started me in the foreground! You must start me in the background (by 
appending '&' to the command) to get the flag!
hacker@processes~starting-backgrounded-processes:~$ /challenge/run &
[1] 147
hacker@processes~starting-backgrounded-processes:~$ 


Yay, you started me in the background! Because of that, this text will probably 
overlap weirdly with the shell prompt, but you're used to that by now...

Anyways! Here is your flag!
pwn.college{APsaYl4_zwZVBdURybYZ3TZw-VU.QX5QDO0wSMwEzNzEzW}

[1]+  Done                    /challenge/run
hacker@processes~starting-backgrounded-processes:~$ 
```
### Steps

The challenge expected me to start the program directly in the background. I launched the program so it would run detached from the terminal prompt, verified that it was running in the background, and then observed it deliver the flag while my prompt remained usable.

### What I Learned

I learned how starting a program in the background allows the shell prompt to remain available immediately and how background processes can still produce output that interleaves with terminal input. I also learned to monitor job completion and retrieve outputs from backgrounded tasks.

### References
same

## 10. Process exit codes
```
hacker@processes~process-exit-codes:~$ /challenge/get-code
Exiting with an error code!
hacker@processes~process-exit-codes:~$ echo $?
231
hacker@processes~process-exit-codes:~$ /challenge/submit-code $?
Incorrect... Make sure to use $? immediately after running /challenge/get-code. 
Your shell will overwrite the $? variable with the exit value of any other 
command you run!
hacker@processes~process-exit-codes:~$ /challenge/get-code $?
Exiting with an error code!
hacker@processes~process-exit-codes:~$ echo $?
222
hacker@processes~process-exit-codes:~$ /challenge/submit-code $?
Incorrect... Make sure to use $? immediately after running /challenge/get-code. 
Your shell will overwrite the $? variable with the exit value of any other 
command you run!
hacker@processes~process-exit-codes:~$ /challenge/222 $?
bash: /challenge/222: No such file or directory
hacker@processes~process-exit-codes:~$ /challenge/get-code && /challenge/submit-code $?
Exiting with an error code!
hacker@processes~process-exit-codes:~$ /challenge/get-code
/challenge/submit-code $?
Exiting with an error code!
CORRECT! Here is your flag:
pwn.college{wJZTS-nznKV5c6pG1q8OZkzoGdY.QX5YDO1wSMwEzNzEzW}
hacker@processes~process-exit-codes:~$ 
```
### Steps

I executed the program that exits with a nonzero status to get the exit code. I captured the exit code immediately using the special shell variable that holds the previous command’s exit status, and then supplied that exact numeric code back to the challenge to verify the result and receive the flag. I made sure not to run any other command in between, to avoid overwriting the captured exit code.

### What I Learned

I learned that every process returns an exit code (0 for success, nonzero for error) and that shells store the most recent exit status in a special variable. I also learned the importance of using that special variable immediately, because any intervening command will overwrite it. This taught me how to programmatically capture and forward exit codes reliably.

### References
Shell documentation on exit status and $? variable
