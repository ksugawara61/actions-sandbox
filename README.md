# actions-sandbox

Github Actionsの検証用リポジトリ

## Environments

name | reviewrs
:--- | :---
Release | ksugawara61

## 検証結果

- Envrionmentsのprotection rulesにreviewersを追加すれば手動承認を挟んでリリースすることができる
- 同じEnvironmentsを別々のJobに設定している場合はapproveをすると止まっているタイミングが同じJobは同時に実行される
  - ↑なので分岐させたい場合は複数のJobごとにEnvironmentを分ける必要がある
- Releaseトリガーの場合ブランチ名はタグ名（ex: release/v1.0.0）になる
- Environment variablesを設定した場合は　${{ vars.MY_ENV }} のようにvarsを利用する
- Envrionmentsを設定していないJob内でEnvironmentsのSecretを使用するこはできない
- branch protection rulesでは正規表現で部分一致を指定可能
- Github Releaseのテンプレートはないらしい
  - [Issue と PRのテンプレートのみサポート](https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/about-issue-and-pull-request-templates)

## 参考URL

- https://zenn.dev/matken/articles/approve-deployments-with-github-environments
- https://stackoverflow.com/questions/56798253/release-template-for-github