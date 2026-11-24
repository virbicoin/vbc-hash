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
| **vbc-pool** | マイニングプール | `../vbc-pool` | [github.com/virbicoin/vbc-pool](https://github.com/virbicoin/vbc-pool) |
| **vbc-rpc** | RPC ノードステータス & JSON-RPC プロキシ | `../vbc-rpc` | [github.com/virbicoin/vbc-rpc](https://github.com/virbicoin/vbc-rpc) |
| **vbc-hash** ← 本リポジトリ | Ethash アルゴリズム実装（C/Go バインディング） | `../vbc-hash` | [github.com/virbicoin/vbc-hash](https://github.com/virbicoin/vbc-hash) |

### 依存関係

- このワークスペースのリポジトリは現在どれも本ライブラリを import していない（2026-11 時点）。
  Gvbc は `consensus/ethash` の自前実装、vbc-pool は `proxy/miner.go` の純 Go 実装で Ethash を検証する
- `go.mod` のモジュールパスは fork 元の `github.com/fedimoss/ethereum-ethash` のまま。
  `github.com/virbicoin/vbc-hash` として `go get` するとパス不一致で失敗するので、使う側は
  `replace github.com/fedimoss/ethereum-ethash => github.com/virbicoin/vbc-hash <version>` で参照する
