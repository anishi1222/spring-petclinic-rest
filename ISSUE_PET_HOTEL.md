# GitHub Issue: ペットホテル機能の追加

このファイルはGitHubでIssueを作成する際に使用する内容です。
GitHubリポジトリで「工程1: 要求開発」テンプレートを使用してIssueを作成してください。

---

## タイトル
```
[要求] ペットホテル予約機能
```

## ラベル
- `phase:requirement`
- `status:planning`

---

## 機能名
```
ペットホテル予約機能
```

## 概要
```
ペットクリニックを訪れる飼い主が旅行や出張中にペットを預けられるよう、ペットホテルの予約・滞在管理機能を提供する。既存のVisitパターンに倣い、チェックイン/チェックアウト管理、部屋番号管理、ステータス管理をREST APIで実現する。
```

## 背景
```
- ペットクリニックを訪れる飼い主から、旅行や出張中にペットを預かってほしいという要望が多く寄せられている
- 現在のVisitエンティティは診察記録の管理のみで、宿泊予約には対応していない
- ペットホテルサービスを提供することで、クリニックの収益源を拡大し、顧客満足度を向上させることができる
- 競合他社のペットクリニックでは既にペットホテルサービスを提供しているケースが多い
```

## ユーザーストーリー
```
- ペットオーナーとして、ペットを預ける予約をしたい、なぜなら旅行や出張中にペットの世話を専門家に任せたいから
- ペットオーナーとして、予約状況（予約済み、チェックイン済み、チェックアウト済み）を確認したい、なぜなら安心してペットを預けたいから
- クリニックスタッフとして、予約一覧を確認したい、なぜなら部屋の空き状況を管理し、適切に予約を受け付けたいから
- クリニックスタッフとして、チェックイン・チェックアウト処理をしたい、なぜなら滞在状況を正確に記録し、料金計算に活用したいから
- システム管理者として、既存のREST API設計パターンに従った実装をしたい、なぜなら保守性と一貫性を保ちたいから
```

## 機能要件
```
- ペットホテル予約情報を登録できる（ペット、チェックイン日、チェックアウト日、部屋番号、ステータス）
- 予約一覧を取得できる（全予約、特定ペットの予約、日付範囲での検索）
- 予約詳細を取得できる（ID指定）
- 予約情報を更新できる（日付変更、部屋番号変更、ステータス更新）
- 予約を削除できる（キャンセル処理）
- ステータス管理ができる（RESERVED：予約済み、CHECKED_IN：チェックイン済み、CHECKED_OUT：チェックアウト済み、CANCELLED：キャンセル済み）
- REST APIでCRUD操作を提供する（GET、POST、PUT、DELETE）
- OpenAPI仕様書に定義を追加する
```

## 非機能要件
```
- 既存のコード構造とパターンに従う（Visit、Pet、Ownerのパターンを参考）
- Spring Data JPAを使用したリポジトリパターンを採用する
- MapStructを使用したEntity/DTOマッピングを実装する
- 適切なバリデーションを含む（@NotNull、日付チェック等）
- RESTful API設計原則に従う
- 適切なHTTPステータスコードを返す（200 OK、201 Created、204 No Content、404 Not Found等）
- セキュリティ設定を既存の実装に従って適用する
- ユニットテストと統合テストを含める（JaCoCo カバレッジ 85%以上を目標）
- OpenAPI Generator を使用してDTO/APIインターフェースを自動生成する
```

## 受け入れ基準
```
- [ ] 全ての機能要件が明確に定義されている
- [ ] ユーザーストーリーが具体的で実装可能である
- [ ] 非機能要件が既存システムの設計方針と整合している
- [ ] 既存エンティティ（Pet、Visit）との関係性が明確である
- [ ] REST APIエンドポイントの仕様が定義されている
- [ ] データベーススキーマの概要が想定できる
- [ ] PMレビューが完了している
```

## 既存システムの参考情報
```
### 既存エンティティ
- **Visit**: 診察記録（date, description, pet）
- **Pet**: ペット情報（name, birthDate, type, owner, visits）
- **Owner**: 飼い主情報（firstName, lastName, address, city, telephone, pets）

### 既存パターン
- Entity層: JPA Entity（@Entity、@Table、@ManyToOne等）
- Repository層: Spring Data JPA（JpaRepository継承）
- Service層: ClinicService インターフェース + 実装クラス
- DTO層: OpenAPI Generator による自動生成（*Dto）
- Mapper層: MapStruct による変換（@Mapper）
- Controller層: REST Controller（@RestController、@RequestMapping）
```

## REST API エンドポイント案
```
GET    /api/pethotelstays           - 全予約取得
GET    /api/pethotelstays/{id}      - 予約詳細取得
POST   /api/pethotelstays           - 新規予約作成
PUT    /api/pethotelstays/{id}      - 予約更新
DELETE /api/pethotelstays/{id}      - 予約削除
GET    /api/pets/{petId}/pethotelstays - 特定ペットの予約一覧取得
```

## 次工程への引き継ぎ事項
```
- 基本設計（Phase 2）で以下を詳細化すること:
  - PetHotelStay エンティティの詳細設計
  - データベーススキーマ設計（テーブル定義、インデックス）
  - レイヤー構造の詳細（各クラスの責務）
  - OpenAPI仕様書の詳細定義
- 詳細設計（Phase 3）で以下を実装準備すること:
  - 各メソッドのシグネチャ
  - バリデーションルール
  - エラーハンドリング戦略
```

---

## Issue作成手順

1. GitHubリポジトリに移動
2. 「Issues」タブをクリック
3. 「New issue」をクリック
4. 「工程1: 要求開発」テンプレートを選択
5. 上記内容を各フィールドに入力
6. ラベルを設定: `phase:requirement`, `status:planning`
7. 必要に応じてマイルストーンやアサインを設定
8. 「Submit new issue」をクリック

---

## 補足: コマンドライン（GitHub CLI）での作成例

GitHub CLIがインストールされている場合、以下のコマンドでもIssueを作成できます:

```bash
gh issue create \
  --title "[要求] ペットホテル予約機能" \
  --label "phase:requirement,status:planning" \
  --body-file ISSUE_PET_HOTEL_BODY.md
```

※ ISSUE_PET_HOTEL_BODY.md には上記の各セクション内容を記載してください。
