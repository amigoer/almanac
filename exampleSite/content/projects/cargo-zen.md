---
title: "cargo-zen"
date: 2026-03-20
status: "maintained"
summary: "一个 Rust 工作区脚手架 CLI —— 把多 crate 项目的常见模板和命令收成一条龙。"
tech: ["Rust", "Clap", "Cargo"]
repo: "https://github.com/amigoer/cargo-zen"
---

## 简介

写多 crate Rust 工作区时反复抄同一套配置（`workspace.toml`、CI、`rustfmt`、`clippy.toml`）—— 这工具把那一套打成 template，`cargo zen new` 一条命令就出。

进入维护模式：核心命令稳定，只接 bug fix 和小功能 PR。
