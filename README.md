<p align="center">
  <img src="https://skillicons.dev/icons?i=docker" /> <br/>
  <a href="https://github.com/mateus-sartorio/ssh-honeypot"><kbd>🔵 GitHub</kbd></a>
</p>

# 🍯 ssh-honeypot

Second assignment for the discipline of Computer Security in the Computer Engineering graduation program at Federal University of Espírito Santo.

<br/>


## 🗒️ Pertinent concepts and tooling

### 1. Honeypots

In computer security, honeypots are decoy systems designed to mimic real systems in order to attract cyber attackers. They serve as bait to detect, study, and mitigate unauthorized attempts to critical systems (like servers or databases for example) without putting real assets at risk.

Honeypots are categorized into two main classes: low-interaction or high-interaction.

#### 1.1. Low-interaction

They simulate only basic parts of a system and can detect basic attacks. They require fewer resources and are easier to deploy but don’t provide in-depth data about the attacker's techniques.

#### 1.2. High-interaction

Mimic an entire system or network, offering a full operating system and applications for the attacker to interact with. These provide more detailed insights into an attack but are more resource-intensive and more complex to configure and maitain.

#### 1.3. Cowrie

For this experiment, we are going to use [Cowrie](https://github.com/cowrie/cowrie) to simulate a low-interaction ssh-honeypot, even thou Cowrie is capable of simulating high-interacion honeypots for telnet and ssh environments.



### 2. Protocols for remote terminal access

Protocols for remote terminal access allow users to connect to and manage remote systems over a network, typically through a command-line interface. The two most used protocols for remote terminal access are Telnet and SSH.

#### 2.1. Telnet

Telnet was one of the first protocols used for remote access to command-line interfaces, and allows users to interact with remote systems as if they were directly connected. However, Telnet lacks encryption, meaning that all data, including sensitive information like passwords, is transmitted in plain text. This lack of cryptography makes Telnet vulnerable to eavesdropping and interception, leading to security risks. Due to these vulnerabilities, Telnet has largely been replaced by more secure protocols, mainly SSH.

#### 2.2. Secure Shell (SSH)

SSH is used mainly for the same purposes of Telnet, but employs strong encryption to protect all data transmitted between the client and server, which prevents eavesdropping and interception, making SSH a secure alternative for remote access. Due to its strong cryptographic protections and additional features such as secure file transfers and port forwarding, SSH has become the standard protocol for secure remote connections, mostly replacing Telnet.

For this experiment, we are going to setup a ssh-honeypot, that is, a decoy ssh terminal with weak credentials (commom username and password), and with the help of Medusa, we are going to try and crack the credentials with brute force.


### 3. Bruteforce attacks

To make a brute force attack to a system means to systematically try all possible combinations of passwords or authentication credentials until the correct one is found. Brute force attacks become viable only if the attacker has a pretty good idea of the subset of all combinations that the credentials can assume, and it is not impratically big.

#### 3.1. Medusa

For simulating a brute attack on the decoy ssh host, we are going to use [Medusa](https://github.com/jmk-foofus/medusa), and automated tool that allows us to easily create an test multiple credentials combinations based on patterns that we can define.

<br>


## ⚙️ Try it for yourself



### Requirements:

- Docker ([Instalation instructions for each operating system](https://docs.docker.com/engine/install))
- Cowrie ([Instalation instructions](https://github.com/cowrie/cowrie))
- Crunch ([]())
- Medusa ([Instalation instructions](https://github.com/jmk-foofus/medusa))

Clone the repository locally. Then, navigate to the directory of the cloned repository:

```bash
git clone https://github.com/mateus-sartorio/ssh-honeypot
cd ssh-honeypot
```

For running Cowrie, we can choose between configuring it to run natively or throuh a docker container. We went with th docker container, and highly recommend you to do the same, as it much faster and simpler, much less likely to run into any problems, and it allows us to concentrate on the experiment itself.

Cowrie provides us with a docker image, that we can configure when creating a container from it. To do so, we can use some default configuration files that should be placed inside a volume. For this experiment, we need only `userdb.txt`, that can be found inside `etc` folder. All other configuration files should be placed here as well. We defined a `root` user with password `ewA9w`.

A list of all possible files and configurations can be found on [Cowrie's official documentation](https://cowrie.readthedocs.io/en/latest/README.html#configuring-cowrie-in-docker).

To start you ssh-honeypot, simply run the following command on the cloned repository root directory:

```bash
docker compose up
```

This should start your decoy ssh host.

```bash
crunch 5 5 qwe ASD 1234567890 -t @@,%@ -o ./wordlist.txt
```

```bash
medusa -h 127.0.0.1 -U ~/Desktop/username -P ~/Desktop/wordlist.txt -M ssh -n 2222
```

```bash
ssh -p 2222 root@localhost
```

<br/>


## ⚖️ License:

Copyright Universidade Federal do Espirito Santo (UFES)

This program is free software: you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.

This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU General Public License for more details.

You should have received a copy of the GNU General Public License along with this program.  If not, see <https://www.gnu.org/licenses/>.

This program is released under license GNU GPL v3+ license.


## 🛟 Support:

Please report any issues with the application at [github.com/mateus-sartorio/ssh-honeypot](https://github.com/mateus-sartorio/ssh-honeypot).