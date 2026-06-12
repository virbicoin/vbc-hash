# CLAUDE.md

このファイルは、Claude Code (claude.ai/code) がこのリポジトリのコードを扱う際のガイドラインを提供します。

## プロジェクト概要

Ethash — VirBiCoin（VBC）ネットワークで使用される Ethash Proof-of-Work アルゴリズムの実装。C 言語のコア実装と Go バインディングを提供します。

## 技術スタック

- **コア実装**: C (src/)
- **Go バインディング**: Go 1.17+
- **ビルドシステム**: CMake, Makefile
- **テスト**: Go test

## よく使うコマンド

```bash
# Go テスト
go test ./...

# CMake ビルド
mkdir build && cd build && cmake .. && make
```

## 関連リポジトリ

VirBiCoin エコシステムは以下のリポジトリで構成されています:

| リポジトリ | 役割 | ローカルパス | URL |
|-----------|------|-------------|-----|
| **virbicoin.com** | 公式 Web サイト（メインサイト） | `../virbicoin.com` | [github.com/virbicoin/virbicoin.com](https://github.com/virbicoin/virbicoin.com) |
| **go-virbicoin** | メインクライアント（Gvbc, Go 実装） | `../go-virbicoin` | [github.com/virbicoin/go-virbicoin](https://github.com/virbicoin/go-virbicoin) |
| **open-virbicoin** | Rust クライアント（Ovbc, OpenEthereum フォーク） | `../open-virbicoin` | [github.com/virbicoin/open-virbicoin](https://github.com/virbicoin/open-virbicoin) |
| **vbc-stats** | ネットワーク統計ダッシュボード | `../vbc-stats` | [github.com/virbicoin/vbc-stats](https://github.com/virbicoin/vbc-stats) |
| **vbc-explorer** | ブロックチェーンエクスプローラー | `../vbc-explorer` | [github.com/virbicoin/vbc-explorer](https://github.com/virbicoin/vbc-explorer) |
| **open-virbicoin-pool** | マイニングプール | `../vbc-pool` | [github.com/virbicoin/open-virbicoin-pool](https://github.com/virbicoin/open-virbicoin-pool) |
| **vbc-rpc** | RPC ノードステータス & JSON-RPC プロキシ | `../vbc-rpc` | [github.com/virbicoin/vbc-rpc](https://github.com/virbicoin/vbc-rpc) |
| **vbc-hash** ← 本リポジトリ | Ethash アルゴリズム実装（C/Go バインディング） | `../vbc-hash` | [github.com/virbicoin/vbc-hash](https://github.com/virbicoin/vbc-hash) |

### 依存関係

- **go-virbicoin** → **vbc-hash**: Gvbc が PoW 検証・マイニングに本ライブラリを利用
- **open-virbicoin-pool** → **go-virbicoin** → **vbc-hash**: マイニングプールが間接的に Ethash を使用
