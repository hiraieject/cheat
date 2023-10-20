
# google test チートシート

----
## 基本的なテスト定義と実行

### TEST()

### TEST_F()

### main()

----
## テストフィクスチャとセットアップ/ティアダウン

### SetUp()

### TearDown()

----
## アサーションとエクスペクテーション

### ASSERT_*

### EXPECT_*

----
## 組み合わせテスト

### TEST_P()

### INSTANTIATE_TEST_SUITE_P()

----
## テストのフィルタリングとオプション

- --gtest_filter

- --gtest_repeat

- --gtest_shuffle

----
## テストイベントリスナー

- OnTestProgramStart()

- OnTestIterationStart()

- OnEnvironmentsSetUpStart()

- OnEnvironmentsTearDownStart()

- OnTestProgramEnd()

----
## テスト結果とレポート

- RecordProperty()

----
## その他のユーティリティ

- gtest_skip

- SCOPED_TRACE()
