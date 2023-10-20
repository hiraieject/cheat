# std::vector チートシート

## std::vector 概要
std::vectorは、C++の標準テンプレートライブラリ（STL）に含まれる動的配列を提供するコンテナクラスです。
可変サイズであり、要素の追加や削除が効率的に行えます。配列と同じように、O(1)でランダムアクセスが可能です。
ただし、挿入と削除は位置によってはO(n)の時間がかかる場合があります。内部では連続したメモリ領域が確保されています。

## インクルードファイル

    #include <vector>  // for std::vector
    #include <algorithm>  // for std::fill, std::sort

## std:: なしで使えるようにする

    using std::vector;
    
## 宣言

    std::vector<int> vec;                   // 空の整数ベクタ
    std::vector<int> vec(10);               // 10個の0で初期化
    std::vector<int> vec(10, 1);            // 10個の1で初期化
    std::vector<int> vec{1, 2, 3, 4, 5};    // 初期値を指定

## 要素へのアクセス

    vec[0] = 10;                            // 添字でアクセス
    vec.at(0) = 10;                         // atメソッドでアクセス（範囲チェックあり）
    
    // 範囲外アクセスの検出
    try {
        int value = vec.at(1000);
    } catch (const std::out_of_range& e) {
        std::cerr << "範囲外アクセス: " << e.what() << std::endl;
    }

## ループでの利用

    // 通常のforループ
    for(int i = 0; i < vec.size(); ++i) {
        std::cout << vec[i] << " ";
    }

    // 範囲forループ
    for(const auto& elem : vec) {
        std::cout << elem << " ";
    }

    // Iteratorを使ったループ
    for(auto it = vec.begin(); it != vec.end(); ++it) {
        std::cout << *it << " ";
    }

## メンバアクセス・操作
### 要素の追加

    vec.push_back(100);                 // 末尾に要素を追加
    vec.insert(vec.begin(), 100);       // 先頭に要素を追加（メモリーコピーが発生し、効率が良くない）
    vec.insert(vec.begin() + n, 100);   // n番目に要素を追加（メモリーコピーが発生し、効率が良くない）

### 要素の削除

    vec.pop_back();                     // 末尾の要素を削除
    vec.erase(vec.begin());             // 先頭の要素を削除（メモリーコピーが発生し、効率が良くない）
    vec.erase(vec.begin() + n);         // n番目の要素を削除（メモリーコピーが発生し、効率が良くない）

### 全要素書き換え

    std::fill(vec.begin(), vec.end(), n);   // 値nで全要素を書き換える
    std::fill(vec.begin(), vec.end(), 0);   // 全要素ゼロクリア

### 全要素削除

    vec.clear();                        // 全要素を削除

### サイズ(要素の数)

    size_t size = vec.size();           // ベクタのサイズ(要素の数)
    vec.resize(20);                     // サイズを20に変更（新たな要素は0で初期化）

### 容量確保/確認

    vec.reserve(100);                   // 100要素分の容量を確保
    size_t capacity = vec.capacity();   // 確保済みの容量の取得

### 要素検索

    // 要素が含まれているか確認
    if(std::find(vec.begin(), vec.end(), value) != vec.end()) {
        // value が vec に含まれている
    }

## ベクタ操作

    // 全要素をコピー
    anotherVec = vec;

    // ベクタ(vec)の後ろにベクタ(addVec)の全要素を追加
    vec.insert(vec.end(), addVec.begin(), addVec.end());

    // ベクタの要素をソート
    std::sort(vec.begin(), vec.end());

    // ベクタの要素を逆ソート
    std::sort(vec.rbegin(), vec.rend());

    // ベクタの入れ替え
    vec1.swap(vec2);                    // 他のベクタと要素を入れ替える
    
## 先頭アドレスの取得

    ptr = vec.data();                   // std::vectorによるメモリ再確保により、
                                        // アドレスが変わる可能性があるので注意

## テンプレート関連

    std::vector<double> vecDouble;          // double型
    std::vector<std::string> vecString;     // std::string型
    std::vector<std::vector<int>> vec2D;    // 2次元ベクタ

