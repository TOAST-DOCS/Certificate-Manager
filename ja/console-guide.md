## Management > Certificate Manager > コンソール使用ガイド
コンソール使用ガイドではCertificate Managerを使用するのに必要な基本的な内容を説明します。
* 通知グループ
* 証明書
* ドメイン
* ユーザーデータ
* 証明書照会/ダウンロードAPI資格関連

## 通知グループ

Certificate Managerは、通知グループ単位で有効期限の通知周期を設定し、通知を受け取る対象者を管理します。

![alarmgroup-1.png](http://static.toastoven.net/prod_certificate_manager/202002/alarmgroup-1.png)

### 通知グループ作成

1. 通知グループメイン画面で**+グループ作成**ボタンをクリックします。
![alarmgroup-2.png](http://static.toastoven.net/prod_certificate_manager/202002/alarmgroup-2.png)
2. **グループ作成**ウィンドウでグループ名を入力します。すでに存在する名前は指定できません。
3. 通知を使用するかどうかを選択します。通知グループに属しているユーザーに有効期限の通知を含むすべての通知を送信するかどうかを選択できます。
4. **追加**ボタンをクリックします。

### 詳細情報

1. 通知グループメイン画面で**詳細情報**ボタンをクリックすると、通知グループ名と通知使用有無、管理データが表示されます。**管理data**は該当通知グループに連携されている証明書、ドメイン、ユーザーデータを意味します。
2. **修正**ボタンをクリックして通知グループの名前および通知を使用するかどうかを変更できます。

![alarmgroup-3.png](http://static.toastoven.net/prod_certificate_manager/202002/alarmgroup-3.png)

### 通知設定

1. 通知グループメイン画面で**通知設定**ボタンをクリックします。
2. 基本に設定されている通知ポリシーがないため、**通知設定**ウィンドウで通知ポリシーを追加すると、有効期限の通知を受け取ることができます。![alarmgroup-4.png](http://static.toastoven.net/prod_certificate_manager/202002/alarmgroup-4.png)

### 通知追加

1. **通知設定**ウィンドウ左下の**+**ボタンをクリックします。![alarmgroup-5.png](http://static.toastoven.net/prod_certificate_manager/202002/alarmgroup-5.png)
2. **通知開始D-day**で、証明書、ドメイン、データ有効期限の何日前から通知を送信するかを指定します。
3. **通知周期**で、何日間隔で通知を送信するかを指定します。
4. **Emailを送信するかどうか**と**SMSを送信するかどうか**で通知送信時にメール、SMSを使用するかどうかを選択します。どちらも選択されていない場合は通知を送信しません。
5. **管理**列で**-**ボタンをクリックして通知ポリシーを削除できます。
6. **通知開始D-day**と**通知周期**は重複して設定できません。
7. **完了**ボタンをクリックします。
![alarmgroup-6.png](http://static.toastoven.net/prod_certificate_manager/202002/alarmgroup-6.png)

### 受信グループ連携画面

通知グループメイン画面で**受信グループ**ボタンをクリックすると、通知グループに連携されているユーザーが表示されます。
デフォルト値には通知グループを作成したユーザーが追加されています。

NHN Cloudプロジェクトに属しているメンバーが通知グループのユーザーに連携される場合があります。![alarmgroup-7.png](http://static.toastoven.net/prod_certificate_manager/202002/alarmgroup-7.png)

### ユーザー追加

上部のユーザー連携検索ウィンドウで、NHN Cloudプロジェクトに属しているメンバーを検索して追加できます。

![alarmgroup-8.png](http://static.toastoven.net/prod_certificate_manager/202002/alarmgroup-8.png)
![alarmgroup-9.png](http://static.toastoven.net/prod_certificate_manager/202002/alarmgroup-9.png)

* **Type**は、そのユーザーが持つNHN Cloudプロジェクトの権限(ADMIN/MEMBER)を意味します。
* メンバーの**名前**、**Email**および**Phone**を確認できます。
* 登録された携帯電話番号がない場合は、**Phone**に「-」と表示されます。この場合、SMS通知の送信が失敗し、通知の送信に失敗すると通知グループに属しているADMINに「通知送信失敗」通知が送信されます。

## 証明書

証明書のドメイン名(例：\*.toast.com)と有効期限を入力すると、連携した通知グループの通知ポリシーに従ってユーザーに通知を送信します。

証明書ファイル(.pem)をアップロードすると、証明書ファイルから下記の項目を自動的に収集します。
* 作成日
* 有効期限
* 証明書の署名方式(例: sha256RSA)
* 認証機関(例：Digicert)

証明書のインストール情報を登録する場合、証明書インストール情報のIPと、ポートから証明書をインポートし、Certificate Managerに登録した証明書と有効期限を比較します。
Certificate Managerに登録した証明書の有効期限より、自動収集した証明書インストール情報の有効期限が前の場合、証明書の交換が必要という通知を送信します。

### メイン画面
メイン画面では証明書リストや有効期限までの残り日数などを確認できます。

![certificate-1.png](http://static.toastoven.net/prod_certificate_manager/202302/certificate-1.png)

* 既に登録している証明書のリストを確認および検索できます。
* 有効期限までの残り日数を確認できます。
* 有効期限を過ぎたデータは赤色で、有効期限までの残り日数が30日以下のデータはオレンジ色で表示されます。

### 証明書の作成

1. 証明書メイン画面で**+証明書の追加**ボタンをクリックすると、**証明書の追加**ウィンドウが表示されます。
![certificate-2.png](http://static.toastoven.net/prod_certificate_manager/202302/certificate-2.png)
2. **通知グループ**で連携する通知グループを選択します。作成された通知グループがない時はリストに表示されず、証明書を作成できません。
3. **名前**に証明書名(CommonName、CN)を入力します。証明書名は重複して登録できません。 <br>
   * SAN証明書の場合、証明書ファイルをアップロードすると証明書名とサブ証明書名が自動的に入力されます。証明書の名前は任意に変更できません。
4. **タイプ**で項目を選択します。
   * Singleは単一証明書です。
   * Wildcardは\*(asterisk)で始まる汎用証明書(複数のホストで使用できる証明書)を意味します。
   * SANは1つの証明書で複数のドメインにSSLを適用できる証明書です。
5. **証明書の登録**下記の**証明書**から証明書ファイルを登録します。<br>
 証明書は必須値ではないため、後で登録しても構いません。
   * 証明書は秘密鍵と証明書で構成された.pem形式のファイルです。
    * サポートする証明書ファイル(.pem)形式は[**問題解決ガイド > 証明書ファイルフォーマット変換**](http://gov-docs.toast.com/ko/Management/Certificate%20Manager/ko/troubleshooting-guide/#_1)をご覧ください。
    * 証明書ファイルは最大512KBまでアップロードできます。
6. **パスフレーズ**(passphrase、秘密文言)に証明書ファイルに含まれる秘密鍵のパスフレーズ(passphrase、秘密文言)を入力します。
7. **追加**ボタンをクリックします。
   * SingleとWildcardの場合は1つの証明書が作成されます。
   * SANの場合、代表証明書とサブ証明書の両方が作成されます。例えば代表証明書が1つ、サブ証明書が3つの場合、合計4つの証明書が作成されます。
8. [Network > Load Balancer](https://gov.toast.com/kr/service/network/load-balancer)製品とリンクする必要がある場合は、パスフレーズ（passphrase、秘密文言）を削除する必要があります。
   * 次のコマンドを使用してパスフレーズを削除できます。
    ```bash
    openssl rsa -in my_private_input.key -out my_private_output.key
    ```


### 詳細画面

1. 証明書メイン画面で**詳細情報**ボタンをクリックすると、証明書ファイル情報を確認できます。
    * **(自動収集)**が表示されたフィールドは証明書ファイルから自動収集された項目を意味します。証明書ファイルが登録されていない場合は「-」と表示されます。
2. **修正**ボタンをクリックすると、証明書情報の修正や、証明書ファイルのアップロードを行うことができます。
    * 証明書名は修正できません。証明書名を修正するには、登録している証明書を削除して新たに作成する必要があります。
      ![certificate-3.png](http://static.toastoven.net/prod_certificate_manager/202002/certificate-3.png)

### 証明書使用情報、インストール情報作成

1. 証明書メイン画面で**証明書の使用情報**ボタンをクリックすると、証明書の使用およびインストール情報を確認できます。デフォルト値では何も登録されていません。
![certificate-4.png](http://static.toastoven.net/prod_certificate_manager/202002/certificate-4.png)
2. **修正**ボタンをクリックすると、次のような画面を確認できます。
![certificate-5.png](http://static.toastoven.net/prod_certificate_manager/202002/certificate-5.png)
3. 右上の**+追加**ボタンをクリックすると、情報を入力できるフィールドが表示されます。
![certificate-6.png](http://static.toastoven.net/prod_certificate_manager/202002/certificate-6.png)
4. 証明書使用情報の名前を入力します。
    * 証明書タイプが**Single**の場合、証明書名と同じにする必要があります。
    * 証明書タイプが**Wildcard**の場合、'\*'(asterisk)を除いた証明書名と同じか、'\*'(asterisk)を除いた'.[証明書名]'で終わる必要があります。
    * 証明書タイプが**SAN**の場合
      * 証明書名がSingle形式の場合、証明書と同じでなければなりません。
      * 証明書名がWildcard形式の場合、'\*'(asterisk)を除外した証明書名と同じか。'\*'(asterisk)を除外した'.[証明書名]'で終わる必要があります。
5. **通知使用有無**で証明書使用情報の通知を使用するかどうかを選択します。
6. 証明書インストール情報を入力するには証明書インストール情報の横にある**+追加**ボタンをクリックします。 
![certificate-7.png](http://static.toastoven.net/prod_certificate_manager/202002/certificate-7.png)
    * **IPアドレス**と**ポート番号**を入力します。証明書の自動収集を使用する場合、入力したIPアドレスとポート番号で証明書をダウンロードして有効期限を比較します。
    * IPアドレスがプライベートIP(例：192.168.0.1, 172.20.0.1, 10.0.0.1)の場合、証明書をダウンロードできず、自動収集失敗通知が送信される場合があります。
7. **完了**ボタンをクリックすると、設定した証明書の使用およびインストール情報が保存されます。

### 証明書使用情報画面
証明書メイン画面で**証明書使用情報**ボタンをクリックすると、証明書使用およびインストール情報を確認できます。
右上の全体/使用/未使用で証明書使用情報の通知使用有無を選択して確認できます。

![certificate-8.png](http://static.toastoven.net/prod_certificate_manager/202002/certificate-8.png)

## ドメイン
DNSの最上位ドメイン名(例：toast.com)と有効期限を入力すると、連携した通知グループの通知ポリシーに合わせてユーザーに通知を送信します。

ドメインの「自動収集」機能を使用する場合、whoisサーバーからドメイン情報を自動収集します。
自動収集する項目は次のとおりです。
* 作成日
* 有効期限
* 登録者(registrar)(例：Gabia, Inc.)
* 登録機関(registrant、ドメインの実所有者)
* ネームサーバー

### メイン画面

登録したドメインリストの確認、検索ができます。

![domain-1.png](http://static.toastoven.net/prod_certificate_manager/202002/domain-1.png)

有効期限まで何日残っているかを確認できます。

有効期限を過ぎたデータは赤色で、有効期限までの残り日数が30日以下のデータはオレンジ色で表示されます。

### ドメイン作成

1. ドメインメイン画面で**+ ドメイン追加**ボタンをクリックします。
![domain-2.png](http://static.toastoven.net/prod_certificate_manager/202002/domain-2.png)
2. **ドメイン追加**ウィンドウで連携する通知グループを選択します。通知グループがない場合はリストに表示されず、ドメインを作成できません。
3. **上位ドメイン情報**の下の**名前**に上位ドメイン名を入力します。上位ドメイン名は重複して登録できません。
4. **有効期限**にドメインの有効期限を入力します。
5. **タイプ**でタイプを選択します。 
    * **サービス用**はDNSサーバーにドメインを登録してサービスで使用する場合です。 
    * **防御用**は、実サービスで使用しないが、サービスの信頼性などの目的でドメインを購入して確保する場合です。
6. **通知使用有無**を選択します。該当ドメインの通知を送信するかどうかを選択します。**未使用**を選択すると該当ドメインの通知が全て送信されません。
7. **自動収集**で項目を自動的に収集するかどうかを選択します。**使用**を選択するとwhoisサーバーから下記の項目を収集します。
    * 作成日
    * 有効期限
    * 登録者(registrar、例：Gabia, Inc.)
    * 登録機関(registrant、ドメインの実所有者)
    * ネームサーバー
8. **サブドメイン情報**でサブドメインの自動収集をするかどうか、およびサブドメイン名を入力します。
    * サブドメインの自動収集を使用する場合、該当ドメインでpingを呼び出し、レスポンスが成功するかどうかを確認します。
    * サブドメイン名は上位ドメインに属している必要があります。
        * サブドメイン名は上位ドメインと同じか、'.[上位ドメイン名]'で終わる必要があります。
        * 例：上位ドメイン名が'toast.com'の場合、サブドメイン名には'toast.com'および'www.toast.com'、'www2.toast.com'などを入力できます。
9. **追加**ボタンをクリックすると、設定したドメイン情報を保存できます。

### 詳細画面

1. ドメインメイン画面で**詳細情報**ボタンをクリックすると、ドメインとサブドメインの情報および自動収集された情報が表示されます。
2. フィールド名の後ろに**(自動収集)**と表示されたフィールドは自動収集された項目を意味します。自動収集された情報がない場合は**-**と表示されます。
3. **修正**ボタンをクリックして上位ドメイン情報を修正したり、登録されたサブドメインの削除またはサブドメインの追加を行うことができます。
    * 上位ドメイン名は修正できません。上位ドメイン名を修正する必要がある場合は、登録したドメインを削除し、新たに作成する必要があります。

![domain-3.png](http://static.toastoven.net/prod_certificate_manager/202002/domain-3.png)

## ユーザーデータ

有効期限があるデータ(例：ライセンスキー)を入力すると、連携した通知グループの通知ポリシーに応じてユーザーに通知を送信します。
特定ユーザーグループに周期的に通知を送信する時に活用できます。

### メイン画面

登録したユーザーデータのリストの確認、検索を行うことができます。有効期限までの残り日数を確認できます。
有効期限を過ぎたデータは赤色で、有効期限までの残り日数が30日以下のデータはオレンジ色で表示されます。

![userdata-1.png](http://static.toastoven.net/prod_certificate_manager/202002/userdata-1.png)

### ユーザーデータの作成

ユーザーデータメイン画面で**+ ユーザーデータ追加**ボタンをクリックすると、次のような画面が表示されます。

![userdata-2.png](http://static.toastoven.net/prod_certificate_manager/202002/userdata-2.png)

* 連携する通知グループを選択します。通知グループが作成されていない場合、選択可能な通知グループが表示されず、ユーザーデータを作成できません。
* ユーザーデータ名を入力します。ユーザーデータ名は重複して登録できません。
* 通知を送信するかどうかを選択します。該当ユーザーデータに対する通知を送信するかどうかを選択できます。該当フィールドを**未使用**に選択する場合、該当ユーザーデータに対する通知が全て送信されません。
* ユーザーデータの有効期限を入力します。
* **追加**ボタンをクリックすると、ユーザーデータ情報が保存されます。

### 詳細画面

ユーザーデータメイン画面で**詳細情報**ボタンをクリックすると、保存していたユーザーデータの情報が表示されます。

**修正**ボタンをクリックしてユーザーデータの情報を修正できます。

![userdata-3.png](http://static.toastoven.net/prod_certificate_manager/202002/userdata-3.png)

## 証明書照会/ダウンロードAPI資格関連 

#### User Access Key ID, Secret Access Key作成

コンソール右上のID領域をクリックすると、次のような**APIセキュリティ設定**メニューを確認できます。

![console-guide-api1](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_certificate_manager/202403_en/console-guide-api1.png)

**APIセキュリティ設定**で**User Access Key ID生成**をクリックしてCertificateManager APIヘッダに入力しなければならない **User Access Key ID**と **Secret Access Key**を生成できます。

![console-guide-api2](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_certificate_manager/202403_en/console-guide-api2.png)

![console-guide-api3](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_certificate_manager/202403_en/console-guide-api3.png)

**User Access Key ID**、**Secret Access Key**を生成すると、下記のように**秘密鍵発行完了**画面が表示されます。秘密鍵は該当ポップアップ画面で一度だけ表示されるるので、この値を記録して使います。

![console-guide-api4](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_certificate_manager/202403_en/console-guide-api4.png)

API リクエスト時に必要な**User Access Key ID**は、秘密鍵発行完了ポップアップを閉じると確認できます。

![console-guide-api5](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_certificate_manager/202403_en/console-guide-api5.png)
