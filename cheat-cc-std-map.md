# std::map チートシート

## std::map 概要
std::mapは、C++の標準テンプレートライブラリ（STL）に含まれるキーと値のペアを管理する連想コンテナです。
通常、内部的にはバランス木が使用されているため、キーに対する挿入、検索、削除がO(log n)で行えます。
要素はキーによってソートされて保持されます

## インクルードファイル

    #include <map>       // for std::map
    #include <algorithm> // for std::for_each

## std:: なしで使えるようにする

    using std::map;

## 宣言

    std::map<int, std::string> m;                           // 空のmap
    std::map<int, std::string> m{{1, "one"}, {2, "two"}};   // 初期値を指定

## 要素へのアクセス

    m[1]    = "one";  // 添字でアクセス（キーが存在しない場合は新規に作成される）
    m.at(1) = "one";  // atメソッドでアクセス（キーが存在しない場合は例外が投げられる）

添字によるアクセスで、存在しないキーを指定しても要素が追加される動作となり、例外は発生しません

## 要素の追加・削除

    m.insert({3, "three"});     // 要素を追加
    m.erase(3);                 // キーが3の要素を削除

## 要素の検索

    auto it = m.find(1);  // キーが1の要素を検索
    if(it != m.end()) {
        // 見つかった
    }

## ループでの利用

    // 通常のforループ
    for(auto it = m.begin(); it != m.end(); ++it) {
        std::cout << it->first << ": " << it->second << std::endl;
    }

    // 範囲forループ
    for(const auto& [key, value] : m) {
        std::cout << key << ": " << value << std::endl;
    }

## サイズと容量

    size_t size = m.size();  // 要素の数
    bool empty = m.empty();  // 空かどうか

## 全要素削除

    m.clear();  // 全要素を削除


## マップ操作

    // 全要素をコピー
    anotherMap = map;

    // 他のマップ(anotherMap)の全要素を後ろに追加
    map.insert(anotherMap.begin(), anotherMap.end());

    // マップの入れ替え
    map1.swap(map2);

## mapの入れ子(2次元連想記憶配列として使う)

    // 初期値付きで宣言
    std::map<int, std::map<std::string, int>> map2D = {
        {1, {{"apple", 100}, {"banana", 200}}},
        {2, {{"apple", 150}}}
    };

    // 要素の書き換え(追加も同じ)
    map2D[1]["apple"]  = 1100;
    map2D[1]["banana"] = 1200;
    map2D[2]["apple"]  = 1150;

    // 要素へのアクセス
    std::cout << map2D[1]["apple"] << std::endl;  // 出力: 100
    std::cout << map2D[1]["banana"] << std::endl; // 出力: 200
    std::cout << map2D[2]["apple"] << std::endl;  // 出力: 150

## 比較オペレーターを持たない型をキーに指定する

カスタム比較関数を提供することで、operator<を持たない型でもキーとして扱うことが可能

    // カスタム比較関数
    struct MyCompare {
        bool operator()(const MyType& a, const MyType& b) const {
            // ここでaとbを比較するロジックを記述
            // 引数aが引数bより小さい場合にtrueを返すように記述する
        }
    };
    std::map<MyType, ValueType, MyCompare> myMap;
