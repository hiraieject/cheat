# std::vector チートシート

## インクルードファイル

    #include <vector>  // 必要なヘッダーファイル

## 宣言

    std::vector<int> vec;  // 空の整数ベクタ
    std::vector<int> vec(10);  // 10個の0で初期化
    std::vector<int> vec(10, 1);  // 10個の1で初期化
    std::vector<int> vec{1, 2, 3, 4, 5};  // 初期値を指定

## 要素へのアクセス

    vec[0] = 10;  // 添字でアクセス
    vec.at(0) = 10;  // atメソッドでアクセス（範囲チェックあり）

## ループでの利用
### 通常のforループ

    for(int i = 0; i < vec.size(); ++i) {
        // 処理
    }

### 範囲forループ

    for(const auto& elem : vec) {
        // 処理
    }

### Iteratorを使ったループ

    for(auto it = vec.begin(); it != vec.end(); ++it) {
        // 処理
    }

## メンバアクセス・操作
### 要素の追加

    vec.push_back(100);  // 末尾に要素を追加

### 要素の削除

    vec.pop_back();  // 末尾の要素を削除

### サイズ取得

    size_t size = vec.size();  // ベクタのサイズ

### 容量確保

    vec.reserve(100);  // 100要素分の容量を確保

### サイズ変更

    vec.resize(20);  // サイズを20に変更（新たな要素は0で初期化）

### 全要素削除

    vec.clear();  // 全要素を削除

### 要素の挿入

    vec.insert(vec.begin() + 1, 42);  // インデックス1に42を挿入

### 要素の削除

    vec.erase(vec.begin() + 1);  // インデックス1の要素を削除

## テンプレート関連

    std::vector<double> vecDouble;  // double型
    std::vector<std::string> vecString;  // std::string型
    std::vector<std::vector<int>> vec2D;  // 2次元ベクタ
