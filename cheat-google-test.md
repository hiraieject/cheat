
# google test チートシート


----
## 基本的なテスト定義と実行

----
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


----
## main()

main()関数は、Google Test フレームワークでテストを実行する際のエントリーポイントとなります。  
この関数は特に::testing::InitGoogleTest()とRUN_ALL_TESTS()という二つの重要な関数呼び出しを含むのが一般的です。

    int main(int argc, char **argv) {
        ::testing::InitGoogleTest(&argc, argv);
        return RUN_ALL_TESTS();
    }

- ::testing::InitGoogleTest()  
この関数は、Google Test フレームワークを初期化するために使用されます。  
コマンドライン引数を受け取り、テストの実行に関するオプション（フィルタリング、出力形式など）を設定することができます。

- RUN_ALL_TESTS()  
この関数は、定義されている全てのテスト（TEST()やTEST_F()で定義されたもの）を実行します。  
この関数の戻り値は、テストの結果に基づいています。全てのテストが成功すれば0、一つでも失敗すれば非0が返されます。

## 組み込みのmain関数

Google Testには組み込みのmain関数が提供されており、特別な初期化や設定が不要な場合はそれをリンクして main() の実装を省略することが可能です。  
ただし、特定の初期化処理や、コマンドライン引数によるカスタマイズが必要な場合は、独自のmain()を定義する方が柔軟です。

### 使い方
組み込みのmain関数を使用するときは、テストプログラムのリンク時に、「-lgtest_main」で組み込みのmain関数をリンクします。

    $ g++ your_test_source.cpp -lgtest -lgtest_main -pthread -o your_test_executable

### main()との 使い分け
- 独自のmain()を定義する場合：特定の初期化処理が必要、またはコマンドラインオプションでカスタマイズしたい場合。
- 組み込みのmain関数を使用する場合：テストの実行に特別な設定や初期化が不要で、簡素な設定で済ます場合。

使い方やカスタマイズの度合いによって、独自に定義するか組み込みのものを使用するかを選択してください。

----
## アサーションとエクスペクテーション

Google Testには、テスト結果をチェックするためのいくつかのマクロが用意されています。  
これらは大きく`ASSERT_*`と`EXPECT_*`の二種類に分類されます。

### ASSERT_*

| マクロ名       | 説明                                         | 使用例                            |
|----------------|----------------------------------------------|-----------------------------------|
| `ASSERT_TRUE`  | 式が真であることを確認します                 | `ASSERT_TRUE(value);`             |
| `ASSERT_FALSE` | 式が偽であることを確認します                 | `ASSERT_FALSE(value);`            |
| `ASSERT_EQ`    | 二つの値が等しいことを確認します             | `ASSERT_EQ(a, b);`                |
| `ASSERT_NE`    | 二つの値が等しくないことを確認します         | `ASSERT_NE(a, b);`                |
| `ASSERT_LT`    | 第一の値が第二の値より小さいことを確認します | `ASSERT_LT(a, b);`                |
| `ASSERT_LE`    | 第一の値が第二の値以下であることを確認します | `ASSERT_LE(a, b);`                |
| `ASSERT_GT`    | 第一の値が第二の値より大きいことを確認します | `ASSERT_GT(a, b);`                |
| `ASSERT_GE`    | 第一の値が第二の値以上であることを確認します | `ASSERT_GE(a, b);`                |
| `ASSERT_STREQ` | 二つの文字列が等しいことを確認します         | `ASSERT_STREQ(str1, str2);`       |
| `ASSERT_STRNE` | 二つの文字列が等しくないことを確認します     | `ASSERT_STRNE(str1, str2);`       |
| `ASSERT_THROW` | 指定した例外がスローされることを確認します   | `ASSERT_THROW(func(), exc_type);` |

### EXPECT_*

| マクロ名       | 説明                                         | 使用例                            |
|----------------|----------------------------------------------|-----------------------------------|
| `EXPECT_TRUE`  | 式が真であることを確認します                 | `EXPECT_TRUE(value);`             |
| `EXPECT_FALSE` | 式が偽であることを確認します                 | `EXPECT_FALSE(value);`            |
| `EXPECT_EQ`    | 二つの値が等しいことを確認します             | `EXPECT_EQ(a, b);`                |
| `EXPECT_NE`    | 二つの値が等しくないことを確認します         | `EXPECT_NE(a, b);`                |
| `EXPECT_LT`    | 第一の値が第二の値より小さいことを確認します | `EXPECT_LT(a, b);`                |
| `EXPECT_LE`    | 第一の値が第二の値以下であることを確認します | `EXPECT_LE(a, b);`                |
| `EXPECT_GT`    | 第一の値が第二の値より大きいことを確認します | `EXPECT_GT(a, b);`                |
| `EXPECT_GE`    | 第一の値が第二の値以上であることを確認します | `EXPECT_GE(a, b);`                |
| `EXPECT_STREQ` | 二つの文字列が等しいことを確認します         | `EXPECT_STREQ(str1, str2);`       |
| `EXPECT_STRNE` | 二つの文字列が等しくないことを確認します     | `EXPECT_STRNE(str1, str2);`       |
| `EXPECT_THROW` | 指定した例外がスローされることを確認します   | `EXPECT_THROW(func(), exc_type);` |

`ASSERT_*`マクロは条件が満たされない場合、その時点でテストを終了します。  
一方で`EXPECT_*`マクロは条件が満たされなくてもテストは継続され、その後のアサーションもチェックされます。  
どちらを使用するかは、テストの要件に応じて選んでください。

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
