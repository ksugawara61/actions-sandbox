# actions-sandbox

Github Actionsの検証用リポジトリ

## Environments

name | reviewrs | 
:--- | :---
Release | ksugawara61
Release2 | ksugawara61

## 検証結果

### Environments

- Envrionmentsのprotection rulesにreviewersを追加すれば手動承認を挟んでリリースすることができる
- 同じEnvironmentsを別々のJobに設定している場合はapproveをすると止まっているタイミングが同じJobは同時に実行される
  - ↑なので分岐させたい場合は複数のJobごとにEnvironmentを分ける必要がある
- Releaseトリガーの場合ブランチ名はタグ名（ex: release/v1.0.0）になる
- Environment variablesを設定した場合は　${{ vars.MY_ENV }} のようにvarsを利用する
- Envrionmentsを設定していないJob内でEnvironmentsのSecretを使用するこはできない
- Repositoryに紐づくSecretsとの併用は可能

### Release

- Github Releaseのテンプレートはないらしい
  - [Issue と PRのテンプレートのみサポート](https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/about-issue-and-pull-request-templates)
- [branch protection rulesでは部分一致を指定可能](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/defining-the-mergeability-of-pull-requests/managing-a-branch-protection-rule)
  - `release/*` のような設定が必要
  - `^release` はNG
  - `release*` は登録可能 releaseAのようなブランチでは動作するが / 区切りになると動作しない
- 生成処理
  - Relase Note記入後に Generate release notes を実行しても記入内容が消されることはない
  - タイトルも消されない（タグ名にしたい場合は何も記入しない方が良い）
  - 再生成したい場合は一度全て削除する
  -Previous tagはautoにするとおそらく latest release が使用される

## 参考URL

- https://zenn.dev/matken/articles/approve-deployments-with-github-environments
- https://stackoverflow.com/questions/56798253/release-template-for-github
- https://qiita.com/da-sugi/items/ba3cd83e64c689795c50