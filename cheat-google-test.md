
# google test チートシート


----
## 基本的なテスト定義と実行

### TEST()

TEST()マクロは最も基本的なテスト処理のブロックを定義します。

    TEST(TestCaseName, TestName)
    
引数は単なる文字列ですが、クオーテーションでは囲まずに記載します

- 第一引数(TestCaseName)：テストケース名  
    テストケース名は、関連する一連のテストをグループ化するための名前です。

- 第二引数(TestName)：テスト名  
    テスト名は、テストケース内で個々のテストを識別するための名前です。  
    テスト名はそのテストが何を確認するものなのかを簡潔に説明するように選びます。

テスト仕様が大項目と少項目で構成されているなら、それらを当てはめても良いでしょう  

#### 使用例

    // function() のテストケースで、配列で2個値を返すテストの例
    TEST(function_test, test_no_1) {
        std::vector<int> return_val = function();
        EXPECT_EQ(return_val.size(), 2);
        EXPECT_EQ(return_val[0], 1);
        EXPECT_EQ(return_val[1], 1);
    }

テスト処理は、通常のC/C++言語で記載します。  
例外の扱いは通常と異なるものになります(後述)  
目的とするテストの処理と結果の判定は、このブロックに ASSERT_*() や EXPECT_*() などのマクロを使用して記述します(マクロの説明は後述)  

#### 注意点
テストケース名とテスト名の組み合わせは一意でなければなりません(重複不可)  
また、特殊文字は使用できないため英数とアンダースコアでの記載を推奨します  

----
### TEST_F()

TEST_F()マクロは、テストフィクスチャ（テスト環境）を使用したテストを定義します。

    TEST_F(TestCaseName, TestName)

#### TEST()との使い分け
- TEST(): テスト間に依存関係がない、または設定/後処理が不要な場合に使用します  
  要は単純な１関数でテストが完結するものに使用します

- TEST_F(): 複数のテストで共通の設定（SetUp）や後処理（TearDown）が必要な場合、  
  またはテストケース間で何らかの状態（メンバ変数など）を共有する必要がある場合に使用します。

#### 使用例

ユーザーは、前処理と後処理を定義するため、提供されている ::testing::Test クラスを継承したクラスを作成する必要があります  
クラス名は TestCaseName と同じ名前とし、SetUp() と TearDown() を再定義して前処理と後処理を実装します  
TEST_F() の記載は TEST() と同じですが、TEST_F() 実行の前後で前記 SetUp() と TearDown() が実行される点が異なります  
また、TEST_F() は前記クラスのメソッド扱いとなるので、クラスメンバーを参照することができます

    class FooTest : public ::testing::Test {
        protected:
        int some_value;
        void SetUp() override {
            // 前処理を実装
            some_value = 1;
        }
        void TearDown() override {
            // 後処理を実装
        }
    };
    TEST_F(FooTest, TestName) {
        EXPECT_EQ(some_value, 1);
    }

TEST_F()を使用することで、テストケース毎にSetUp()とTearDown()が自動的に呼ばれ、テストの独立性を保ちつつ共通の処理を簡潔に記述できます。
これによってテストコードのDRY（Don't Repeat Yourself）原則にも沿った形になります。

#### 注意点
SetUp()やTearDown()内で生成/消去するリソースは、各テストケースが実行される前後でそれぞれ確保/解放されます。  
テストケース名がTEST_F()と同一のテストフィクスチャクラスを継承する必要があります。  
以上のような特性を持つため、TEST_F()は複数のテストで共通の設定や後処理、状態を共有する必要がある場合に非常に有用です。


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

---
以下でオンライン参照できます  
https://github.com/hiraieject/cheat/blob/main/cheat-google-test.md
