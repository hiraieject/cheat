
# google test チートシート

このファイルはマークダウン形式され、以下で参照できます

https://github.com/hiraieject/cheat/blob/main/cheat-google-test.md

----
## 基本的なテスト定義と実行

### TEST()

TEST()マクロは最も基本的なテスト処理のブロックを定義します。

    TEST(TestCaseName, TestName)

- 第一引数(TestCaseName)：テストケース名  
    テストケース名は、関連する一連のテストをグループ化するための名前です。

- 第二引数(TestName)：テスト名  
    テスト名は、テストケース内で個々のテストを識別するための名前です。  
    テスト名はそのテストが何を確認するものなのかを簡潔に説明するように選びます。

テスト仕様が大項目と少項目で構成されているなら、それらを当てはめても良いでしょう  
テストケース名とテスト名の組み合わせは一意(重複不可)でなければなりません  
特殊文字は使用できないため、英数とアンダースコアでの記載を推奨します  

    // 仕様例 (functionのテストケースで、テスト番号1とした場合の例)
    TEST(function_test, test_no_1) {
        array = function();
        EXPECT_EQ(array[0], 1);
        EXPECT_EQ(array[1], 1);
    }

テスト処理は、通常のC/C++言語で記載します。  
例外の扱いは通常と異なるものになります(後述)  
目的とするテストの処理と結果の判定は、このブロックに ASSERT_*() や EXPECT_*() などのマクロを使用して記述します(マクロの説明は後述)  

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
