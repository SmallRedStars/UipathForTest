# UiPath Orchestrator 組織管理・権限付与手順書

**対象バージョン:** UiPath Orchestrator 2023.4 - 2024.10  
**最終更新日:** 2026年1月

---

## 目次

1. [概要](#概要)
2. [組織構造の理解](#組織構造の理解)
3. [ユーザー管理](#ユーザー管理)
4. [グループ管理](#グループ管理)
5. [ロール(権限)管理](#ロール権限管理)
6. [フォルダー管理](#フォルダー管理)
7. [権限の割り当て手順](#権限の割り当て手順)

---

## 概要

UiPath Orchestratorは、オートメーション、ロボット、および関連エンティティを管理するためのUiPath Platformの管理ツールです。テナントとフォルダーの構造により組織構造同様の管理が可能であり、ロールベースのアクセス制御(RBAC)を実装しています。

**参考:** [Orchestrator - アクセス権を管理する](https://docs.uipath.com/automation-suite/lang-ja/docs/managing-access)

---

## 組織構造の理解

### 階層構造

```
組織(Organization)
  └── テナント(Tenant)
      ├── モダンフォルダー(Modern Folder)
      │   └── サブフォルダー(最大6階層)
      └── クラシックフォルダー(Classic Folder)
```

**参考:** [Orchestrator - フォルダー](https://docs.uipath.com/orchestrator/lang-ja/docs/folders)

### 組織レベルとサービスレベルの違い

- **組織レベルロール:** Automation Suite全体のアクセス権を制御
- **サービスレベルロール(テナント/フォルダーロール):** Orchestratorサービス内の権限を制御

**参考:** [アクセス権を管理する](https://docs.uipath.com/automation-suite/lang-ja/docs/managing-access)

---

## ユーザー管理

### 3.1 新規ユーザーの招待

#### 手順:

1. **Automation Cloudにログイン**
   - URL: `https://cloud.uipath.com/`

2. **管理画面に移動**
   - 左側メニューから「管理(Admin)」→「アカウントとグループ(Accounts & Groups)」をクリック

3. **ユーザーを招待**
   - 「ユーザーを招待(Invite Users)」ボタンをクリック
   - 招待するユーザーのメールアドレスを入力
   - 「送信(Send)」をクリック

4. **ユーザー側の対応**
   - 招待されたユーザーは受信メールから「Verify Email」をクリック
   - UiPathアカウントを新規登録(既存アカウントがある場合はログイン)

**参考:** [初めての UiPath Orchestrator 設定](https://qiita.com/hamam/items/f6779e91253f26fcab40)

**参考:** [UiPath Orchestratorのユーザー管理](https://www.cresco.co.jp/blog/entry/entry-5794933950444390087.html)

### 3.2 ライセンスの割り当て

#### 利用可能なライセンスタイプ:

- **Everyone:** デフォルト(開発不可)
- **Automation Users:** Attended実行ライセンス
- **Administrators:** 管理者権限
- **Citizen Developers:** StudioXのみ使用可能
- **Automation Developers:** StudioX & Studio開発ライセンス
- **Automation Express:** 個人ワークスペースでのStudioX開発

#### 手順:

1. **テナントにアクセス**
   - Orchestratorにログイン
   - 該当のテナントを選択

2. **アクセス権を管理ページに移動**
   - 「テナント(Tenant)」→「アクセス権を管理(Manage Access)」→「ロールを割り当て(Assign Roles)」タブ

3. **ユーザーを選択**
   - 対象ユーザーの右端にある「その他のアクション(More Actions)」→「編集(Edit)」

4. **ライセンスを割り当て**
   - 「ライセンスを割り当て(Assign License)」ボタンをクリック
   - 該当のライセンスを選択
   - 「保存(Save)」をクリック

**参考:** [UiPath Orchestratorのライセンス・権限付与](https://www.cresco.co.jp/blog/entry/entry-5794933950444390087.html)

---

## グループ管理

### 4.1 既定のグループ

Orchestratorには以下の既定グループが存在します:

- **Administrators:** 組織管理者ロール + Orchestrator Administratorロール
- **Everyone:** 全ローカルユーザーが自動所属
- **Automation Users:** Attended実行用
- **Automation Developers:** 開発者用
- **Citizen Developers:** StudioXユーザー用

**参考:** [Managing Access and Automation Capabilities](https://docs.uipath.com/orchestrator/standalone/2023.4/user-guide/about-managing-user-access)

### 4.2 カスタムグループの作成

#### 手順:

1. **管理画面に移動**
   - 「管理(Admin)」→「組織名」→「アカウントとグループ(Accounts & Groups)」

2. **グループタブを選択**
   - 「グループ(Groups)」タブをクリック

3. **新規グループ作成**
   - 「グループを追加(Add Group)」をクリック
   - グループ名と説明を入力
   - 「作成(Create)」をクリック

4. **メンバーを追加**
   - 作成したグループを選択
   - 「編集(Edit)」をクリック
   - 「名前(Names)」フィールドでユーザーまたはロボットアカウントを検索
   - 検索結果からアカウントを選択
   - 「保存(Save)」をクリック

**参考:** [Managing accounts and groups](https://docs.uipath.com/orchestrator/standalone/2024.10/user-guide/managing-accounts)

---

## ロール(権限)管理

### 5.1 ロールの種類

#### テナントロール
テナントレベルのリソース(マシン、ユーザー、監査等)に対する権限セット

#### フォルダーロール
フォルダー内のリソース(プロセス、アセット、キュー等)に対する権限セット

**注意:** 混合ロールは非推奨で、新規作成はできません

**参考:** [Orchestrator - ロールを管理する](https://docs.uipath.com/orchestrator/lang-ja/docs/managing-roles)

### 5.2 既定のロール

#### テナントレベル:

| ロール名 | 説明 |
|---------|------|
| Administrator | すべてのテナントレベル権限 |
| Tenant Administrator | テナント管理者権限(Administratorと同等) |
| Allow to be Folder Administrator | フォルダー管理に必要な最小限のテナント権限 |
| Allow to be Automation User | オートメーション実行に必要なテナント権限 |
| Allow to be Automation Developer | 開発に必要なテナント権限 |

**参考:** [Orchestrator - 既定のロール](https://docs.uipath.com/orchestrator/lang-ja/docs/default-roles)

#### フォルダーレベル:

| ロール名 | 説明 |
|---------|------|
| Folder Administrator | フォルダーとサブフォルダーの管理権限 |
| Automation User | プロセス実行に必要なフォルダー権限 |
| Automation Developer | 開発に必要なフォルダー権限 |

**重要:** テナントロールとフォルダーロールは必ずペアで割り当てる必要があります。
- 例: `Allow to be Folder Administrator`(テナント) + `Folder Administrator`(フォルダー)

**参考:** [Orchestrator - 既定のロール](https://docs.uipath.com/orchestrator/lang-ja/docs/default-roles)

### 5.3 カスタムロールの作成

#### 手順:

1. **アクセス権を管理ページに移動**
   - 「テナント(Tenant)」→「アクセス権を管理(Manage Access)」→「ロール(Roles)」タブ

2. **新しいロールを追加**
   - 「新しいロールを追加(Add a new role)」をクリック
   - 「テナントロールを追加」または「フォルダーロールを追加」を選択

3. **ロールを定義**
   - 上部で「新規追加(Add new)」が選択されていることを確認
   - 「名前(Name)」フィールドにロール名を入力(例: Custom Developer)
   - 必要な権限のチェックボックスを選択
     - **V** = 表示(View)
     - **E** = 編集(Edit)
     - **C** = 作成(Create)
     - **D** = 削除(Delete)

4. **ロールを作成**
   - 「作成(Create)」をクリック

**参考:** [Orchestrator - ロールを管理する](https://docs.uipath.com/orchestrator/lang-ja/docs/managing-roles)

### 5.4 ロールのエクスポート/インポート

#### エクスポート手順:

1. 「テナント」→「アクセス権を管理」→「ロール」タブ
2. 対象ロールの行右端「その他のアクション」→「エクスポート(Export)」
3. CSV形式でダウンロード

#### インポート手順:

1. 「テナント」→「アクセス権を管理」→「ロール」タブ
2. 「新しいロールを追加」→ロールタイプを選択
3. 上部で「インポート(Import)」を選択
4. エクスポートしたCSVファイルを選択
5. 「作成(Create)」をクリック

**注意:** 混合ロールはエクスポートできません

**参考:** [Orchestrator - ロールを管理する](https://docs.uipath.com/orchestrator/lang-ja/docs/managing-roles)

---

## フォルダー管理

### 6.1 フォルダーの種類

#### モダンフォルダー:
- ユーザーがフォルダーに割り当てられる
- ロボットは自動プロビジョニング
- 階層構造サポート(最大7階層)

#### クラシックフォルダー:
- プロビジョニングされたロボットを含む
- フラットな構造
- 既存環境からの移行時に使用

**参考:** [フォルダーについて](https://docs.uipath.com/orchestrator/lang-ja/v2020.4/docs/about-folders)

### 6.2 第1レベルフォルダーの作成

#### 手順:

1. **フォルダーページに移動**
   - 「テナント(Tenant)」→「フォルダー(Folders)」

2. **新しいフォルダーボタンをクリック**
   - 「新しいフォルダー(New Folder)」ボタンをクリック

3. **フォルダー情報を入力**
   - **名前(Name):** フォルダー名を入力(例: 経理部、人事部)
   - **説明(Description):** フォルダーの説明を入力
   - **プロセスパッケージのソース(Process package source):**
     - 「テナントのパッケージフィード」: 共通フィード使用(サブフォルダーでも使用可能)
     - 「このフォルダー専用の新しいパッケージフィードを作成」: 専用フィード作成(第1レベルのみ)

4. **フォルダーを作成**
   - 「作成(Create)」をクリック

**参考:** [Orchestrator - フォルダーを管理する](https://docs.uipath.com/orchestrator/lang-ja/docs/managing-folders)

**参考:** [UiPath Orchestratorのフォルダー作成](https://www.cresco.co.jp/blog/entry/entry-5794933950444390087.html)

### 6.3 サブフォルダーの作成

#### 手順:

1. **親フォルダーを選択**
   - 「フォルダー」ページの左側ペインで親フォルダーをクリック

2. **サブフォルダーを追加**
   - フォルダーコンテキスト内で「サブフォルダーを追加(Add Subfolder)」をクリック

3. **サブフォルダー情報を入力**
   - 名前と説明を入力
   - パッケージソースは親フォルダーから継承

4. **作成**
   - 「作成(Create)」をクリック

**注意:** サブフォルダーは最大6階層まで作成可能(ルートフォルダーを含めて全体で7階層)

**参考:** [Orchestrator - フォルダーを管理する](https://docs.uipath.com/orchestrator/lang-ja/docs/managing-folders)

---

## 権限の割り当て手順

### 7.1 テナントレベルでのロール割り当て

#### ユーザーへの割り当て:

1. **アクセス権を管理ページに移動**
   - 「テナント」→「アクセス権を管理(Manage Access)」

2. **ロールを割り当てをクリック**
   - 画面右上の「ロールを割り当て(Assign roles)」→「ユーザー(User)」を選択

3. **ユーザーを検索**
   - 「ユーザーを検索(Search for a user)」ドロップダウンで対象ユーザーを検索・選択

4. **テナントロールを選択**
   - 「ロール(Roles)」フィールドで割り当てるテナントロールを選択
   - 複数選択可能

5. **Webアクセスを設定**
   - 「Webアクセス(Web Access)」トグルでOrchestratorUIへのログイン可否を設定

6. **UIプロファイルを設定**
   - 「UIプロファイル(UI Profile)」でユーザーインターフェイスプロファイルを選択

7. **ロボット設定(オプション)**
   - Attendedロボットを作成する場合は「次へ(Next)」
   - それ以外は「スキップして割り当て(Skip and assign)」

8. **完了**
   - 設定が適用され、ユーザーがテナントレベルの権限を取得

**参考:** [Orchestrator - ロールを割り当てる](https://docs.uipath.com/orchestrator/lang-ja/docs/assigning-roles)

#### グループへの割り当て:

1. 「テナント」→「アクセス権を管理」
2. 「ロールを割り当て」→「グループ(Group)」を選択
3. グループを検索・選択
4. テナントロールを選択
5. Webアクセスとロボット設定を構成
6. 「割り当て(Assign)」または「スキップして割り当て」

**注意:** グループに設定した権限は、そのグループに所属する全メンバーに継承されます

**参考:** [Orchestrator - Assigning Roles](https://docs.uipath.com/orchestrator/standalone/2023.4/user-guide/assigning-roles)

### 7.2 フォルダーレベルでのロール割り当て

#### 手順:

1. **フォルダーページに移動**
   - 「テナント」→「フォルダー」

2. **フォルダーを選択**
   - 左側の「フォルダーを管理(Manage Folders)」ペインで対象フォルダーをクリック

3. **アカウント/グループを割り当て**
   - 右側ダッシュボードで「アカウント/グループを割り当て(Assign Account/Group)」をクリック

4. **アカウントまたはグループを検索**
   - 「アカウントまたはグループの名前」ドロップダウンで対象を検索・選択

5. **フォルダーロールを選択**
   - 「上で選択したアカウント/グループのロール」ドロップダウンでフォルダーロールを選択

6. **自動テナントロール確認**
   - フォルダーロールを割り当てる際、対応するテナントロールを持っているか自動チェック
   - 持っていない場合、テナントロールの割り当てを促すプロンプトが表示
   - その場で割り当てるか、後で割り当てるかを選択可能

7. **割り当てを完了**
   - 「割り当て(Assign)」をクリック

**参考:** [Orchestrator - フォルダーを管理する](https://docs.uipath.com/orchestrator/lang-ja/docs/managing-folders)

**参考:** [フォルダーを管理する](https://docs.uipath.com/orchestrator/lang-ja/v2020.10/docs/managing-folders)

### 7.3 実践例: 部門別権限設定

#### シナリオ:
経理部に所属し人事部も兼務するメンバーに以下の権限を付与:
- 経理部フォルダー: 管理者(プロセスの新規登録・削除)
- 人事部フォルダー: プロセス実行のみ

#### 設定手順:

**Step 1: テナントレベルのロール割り当て**
1. 「テナント」→「アクセス権を管理」
2. 対象ユーザーに以下のテナントロールを割り当て:
   - `Allow to be Folder Administrator`
   - `Allow to be Automation User`

**Step 2: 経理部フォルダーのロール割り当て**
1. 「テナント」→「フォルダー」→「経理部」フォルダーを選択
2. 対象ユーザーに以下のフォルダーロールを割り当て:
   - `Folder Administrator`

**Step 3: 人事部フォルダーのロール割り当て**
1. 「テナント」→「フォルダー」→「人事部」フォルダーを選択
2. 対象ユーザーに以下のフォルダーロールを割り当て:
   - `Automation User`

**結果:**
- 経理部: フォルダー管理権限(プロセス作成・削除可能)
- 人事部: プロセス実行権限のみ

**参考:** [初めての UiPath Orchestrator 設定 - ロール割り当て例](https://qiita.com/hamam/items/f6779e91253f26fcab40)

### 7.4 ロールと権限の確認方法

#### 手順:

1. **テナントレベルのロール確認**
   - 「テナント」→「アクセス権を管理」→「ロールを割り当て」タブ
   - 対象ユーザーまたはグループを選択
   - 「ロールと権限を確認(Check roles & permissions)」をクリック

2. **フォルダーレベルのロール確認**
   - フォルダーコンテキスト内で同様に確認可能

3. **グループからの継承確認**
   - 確認画面では、ロールが直接割り当てられたものか、グループから継承されたものかが表示される

**参考:** [Managing accounts and groups](https://docs.uipath.com/orchestrator/standalone/2024.10/user-guide/managing-accounts)

### 7.5 ユーザー/グループの削除

#### 注意事項:
- Administratorロールを持つユーザーは削除できません
- 実行中のジョブがあるロボットを持つユーザーを削除すると、ジョブが削除されます
- Orchestratorから削除しても、組織からは削除されません

#### 手順:

1. **アクセス権を管理ページに移動**
   - 「テナント」→「アクセス権を管理」→「ロールを割り当て」タブ

2. **対象を選択**
   - 削除するユーザーまたはグループを選択
   - 「その他のアクション(More Actions)」→「削除(Remove)」

3. **確認**
   - 実行中のジョブがある場合、警告メッセージが表示
   - 削除を続行するか、キャンセルするかを選択

4. **完了**
   - ユーザー/グループがOrchestratorから削除され、すべてのロールが取り消される

**参考:** [Orchestrator - ロールを割り当てる](https://docs.uipath.com/orchestrator/lang-ja/docs/assigning-roles)

### 7.6 ユーザーの有効化/無効化

#### 手順:

1. 「テナント」→「アクセス権を管理」→「ロールを割り当て」タブ
2. 対象ユーザーを選択
3. 「その他のアクション」→「有効化(Activate)」または「無効化(Deactivate)」
4. 無効化されたユーザーのOrchestratorアクセスは取り消される

**注意:** 管理者権限を持つユーザーのみがこの操作を実行できます

**参考:** [Orchestrator - Assigning Roles](https://docs.uipath.com/orchestrator/standalone/2023.4/user-guide/assigning-roles)

---

## 付録A: ロール設計のベストプラクティス

### A.1 権限分離の原則

**開発環境と本番環境の分離:**
- 開発者: 開発フォルダーでは管理者権限、本番フォルダーでは閲覧のみ
- 運用担当: 本番フォルダーで管理者権限、開発フォルダーは閲覧のみ

**参考:** [UiPath Orchestratorの権限(ロール)を考えてみる](https://qiita.com/yoshiyuki-iwata/items/2e9741ed5d6a0a1ea756)

### A.2 カスタム開発者ロールの例

#### テナントロール: `Allow to be Developer`

必要な権限:
- パッケージ: V, C, E
- アセット: V, C, E
- ログ: V
- キュー: V, C, E
- トランザクション: V, C, E

#### フォルダーロール: `Developer`

必要な権限:
- プロセス: V(表示のみ、作成は管理者が行う)
- アセット: V, C, E
- キュー: V, C, E

**参考:** [UiPath Orchestratorの権限(ロール)を考えてみる](https://qiita.com/yoshiyuki-iwata/items/2e9741ed5d6a0a1ea756)

### A.3 大規模デプロイの管理

**Active Directoryとの連携:**
- ディレクトリグループをOrchestratorに追加
- グループメンバーシップに基づく自動プロビジョニング
- ログイン時に自動的にロールを継承

**参考:** [Managing Access and Automation Capabilities](https://docs.uipath.com/orchestrator/standalone/2023.4/user-guide/about-managing-user-access)

---

## 付録B: トラブルシューティング

### B.1 よくある問題

**問題:** ユーザーがフォルダーにアクセスできない
**解決策:** 
1. テナントロールとフォルダーロールの両方が割り当てられているか確認
2. Webアクセスが有効になっているか確認
3. グループから継承される権限を確認

**問題:** ロールを削除できない
**解決策:**
1. 削除しようとしているのが混合ロールではないか確認
2. ユーザーが実行中のジョブを持っていないか確認

**問題:** フォルダー階層が表示されない
**解決策:**
1. ユーザーアクセスは親フォルダーから継承されるため、親フォルダーへのアクセス権があるか確認
2. アカウントが割り当てられているフォルダーが1,000を超えていないか確認(パフォーマンス問題)

**参考:** [Orchestrator - フォルダー](https://docs.uipath.com/orchestrator/lang-ja/docs/folders)

### B.2 エラーメッセージ

**"Not found (#1002)"**
- アカウントが組織から削除されている
- Automation Cloud管理画面で再度招待が必要

**参考:** [Orchestrator - ロールを割り当てる](https://docs.uipath.com/orchestrator/lang-ja/v0/docs/assigning-roles)

---

## 付録C: 参考リンク

### 公式ドキュメント:

1. [Orchestrator ユーザーガイド (日本語)](https://docs.uipath.com/orchestrator/lang-ja/docs)
2. [アクセス権を管理する](https://docs.uipath.com/automation-suite/lang-ja/docs/managing-access)
3. [フォルダーを管理する](https://docs.uipath.com/orchestrator/lang-ja/docs/managing-folders)
4. [ロールを管理する](https://docs.uipath.com/orchestrator/lang-ja/docs/managing-roles)
5. [既定のロール](https://docs.uipath.com/orchestrator/lang-ja/docs/default-roles)
6. [ロールを割り当てる](https://docs.uipath.com/orchestrator/lang-ja/docs/assigning-roles)
7. [Managing Access and Automation Capabilities (English)](https://docs.uipath.com/orchestrator/standalone/2023.4/user-guide/about-managing-user-access)
8. [Assigning Roles (English)](https://docs.uipath.com/orchestrator/standalone/2023.4/user-guide/assigning-roles)

### コミュニティリソース:

1. [初めての UiPath Orchestrator 設定 - Qiita](https://qiita.com/hamam/items/f6779e91253f26fcab40)
2. [UiPath Orchestratorのユーザー管理・ライセンス・権限付与について - CRESCO](https://www.cresco.co.jp/blog/entry/entry-5794933950444390087.html)
3. [UiPath Orchestratorの権限(ロール)を考えてみる - Qiita](https://qiita.com/yoshiyuki-iwata/items/2e9741ed5d6a0a1ea756)
4. [Orchestrator導入ステップバイステップガイド](https://www.uipath.com/ja/community-blog/knowledge-base/orchestrator-installation-guide)

---

## 改訂履歴

| 版 | 日付 | 変更内容 |
|----|------|----------|
| 1.0 | 2026-01-29 | 初版作成 |

---

**注意事項:**
- 本手順書は UiPath Orchestrator 2023.4 - 2024.10 を対象としています
- 製品のバージョンアップにより、画面や手順が変更される可能性があります
- 最新情報は必ず公式ドキュメントをご確認ください
- 本番環境での作業前に、必ずテスト環境で動作確認を行ってください

---

**作成日:** 2026年1月29日  
**対象バージョン:** UiPath Orchestrator 2023.4 - 2024.10  
**ドキュメント形式:** Markdown
