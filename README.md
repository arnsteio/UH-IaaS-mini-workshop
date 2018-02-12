# UH-IaaS-mini-workshop

Time: 2 hours
 
Prerequisites: Knowledge of the Linux command line, and SSH key pairs

## Course content:
1. [Background](01-intro.pdf)
2. [Initial login, and making a server](02-makingServer.md)
3. [Let's log in!](03-initialLogin.md)
4. [Attaching storage](04-AttachingStorage.md)
5. [Initializing storage](05-initializingStorage.md)

## Web site:
<https://arnsteio.github.io/UH-IaaS-mini-workshop/>

## Notes on teaching:

First run with this material (the CLI-only workshop) february -18:
* 2 hours is just enough time
* Very helper heavy (one helper per two participants is about right. This is shockingly much)
* Main problems were:
  * Problems installing openstack-cli. Exacerbated with Mac and Windows machines in addition to different Linux flavours.
  * People on Windows machines had some problems uploading SSH keys. 
  * People on Windows machines had problems sending their keys with their initial ssh logins.
  * Making keystone_rc.sh took time for some people.
  * People didn't really have the prerequisites in place. 
* Suggestions for next time:
  * Make sure everyone has GUI access. In practice, make sure only UiO-internal people can sign up :-/
  * Give people access to a linux server with openstack-cli installed. 
  * Consider giving people a finished keystone.rc-file for a test project. Both these last two suggestions would somewhat defeat the point of the workshop, though.
  * Give people access to the Git repo immediately to save people time typing.
* Survey results are in. Participants were happy, this is surprising to me as I though the workshop was heavy going.

To address these issues I've begun adapting and adding back old material to make a new 3-hour workshop at <https://arnsteio.github.io/UH-IaaS-workshop/>.
I'll still teach this 2-hour CLI-only workshop if people wish me to, but I prefer doing either 2-hour mainly CLI or 3-hour GUI and CLI. 
