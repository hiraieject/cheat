
# google test チートシート

このファイルはマークダウン形式され、以下で参照できます

https://github.com/hiraieject/cheat/blob/main/cheat-google-test.md

----
## 基本的なテスト定義と実行

### TEST()
    
    TEST(TestCaseName, TestName) {
        EXPECT_EQ(1, 1);
    }

### TEST_F()

    class FooTest : public ::testing::Test {
        protected:
        void SetUp() override {}
        void TearDown() override {}
    };
    TEST_F(FooTest, TestName) {
        EXPECT_EQ(1, 1);
    }


### main()

    int main(int argc, char **argv) {
        ::testing::InitGoogleTest(&argc, argv);
        return RUN_ALL_TESTS();
    }

----
## テストフィクスチャとセットアップ/ティアダウン

### SetUp()

    void SetUp() override {
        // セットアップ処理
    }

### TearDown()

    void TearDown() override {
        // ティアダウン処理
    }

----
## アサーションとエクスペクテーション

### ASSERT_*

表形式で

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
