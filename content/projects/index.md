---
title: "Projects"
description: "Open source projects and personal experiments"
date: 2025-12-30
---

A collection of my open source projects and personal experiments. Most of these focus on developer tools, systems programming, and productivity.

## ⚡ [clapi.nvim](https://github.com/markelca/clapi.nvim)
**Language:** Lua  
**Frameworks:** telescope.nvim

Neovim plugin to display and navigate the public interface of your modules. Makes it easier to understand and work with large codebases by showing you what's exposed.

{{< figure src="./img/clapi.gif" alt="Second image" >}}

## 🐟[TunaDB](https://github.com/markelca/TunaDB)
**Language:** Rust  
**Frameworks:** clap, tokio

A disk-based key-value store implementation. Built to learn Rust and explore storage engine fundamentals.

### Technical details
It currently uses a simple length-prefixed binary encoding format for storage files and an in-memory byte offset HashMap as its indexing strategy. The server communicates with clients over TCP sockets and uses protocol buffers for data serialization.

Implementation details, including the storage/indexing algorithms and communication protocols, are abstracted and subject to change. There are plans to implement more sophisticated data structures, such as B-Trees and LSM-Trees, in the future, as well as a custom communication protocol.

## 💻 [prioritty](https://github.com/markelca/prioritty)
**Language:** Go  
**Frameworks:** bubbletea

Terminal-based task list and productivity tool. Designed for managing tasks efficiently from the command line.

{{< figure src="./img/prioritty.gif" alt="Second image" >}}

## 🏗️ [aws-web-deploy](https://github.com/markelca/aws-web-deploy)
**Languages:** HCL (Terraform), Ansible

Batteries-included template to deploy web servers on AWS. Leverages Terraform and Ansible to provision and configure the infrastructure. Deploys an Nginx web server on EC2, also configuring the DNS server with Route53, SSH key access, and HTTPS.


## 💬 [chat.ai](https://github.com/markelca/chat.ai)
**Language:** TypeScript  
**Frameworks:** Next.js

Terminal AI chat application with live streaming to a Next.js web UI. Experiments with real-time AI interactions across different interfaces.

## ⚙️ [dotfiles](https://github.com/markelca/dotfiles)
**Language:** Nix

My system configurations for Nix and Neovim. Includes my heavily customized development environment setup.

---

For more projects and details, check out my [GitHub profile](https://github.com/markelca).
