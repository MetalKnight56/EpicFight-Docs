# カスタム3Dアーマーの不具合に関するその他の解決策
※この方法は、ブレンダーで手動でパッチを適用するほど効果的ではない可能性があります。 このページで解説するツールは、主にModパックやMod開発者が鎧をテストするためのものです。 _**[カスタム3Dアーマーリソースパック](armor/page1)**_ の方が確実に不具合を修正できます。


***
## **💡 アーマーデバッグモードを用いて、鎧が正常に表示されるか確認する。**

Minecraft でF3+Y キーを押すと、アーマーデバッグモードを有効にできます。 これによりモデル生成アルゴリズムが実行され、毎フレームごとにアーマーモデルが組み立てられます。 しかし内部処理が増加しfpsが低下するため、通常は機能をOFFにしておくことをオススメします。

![image](https://user-images.githubusercontent.com/79469058/168334604-6542eff4-c77e-4ef2-a71a-79ddeef91a9a.png)

_このメッセージは、アーマーデバッグモードをオンにすると表示されます。_
***
### **📦 アルゴリズムの生成結果をリソースパックとしてエクスポートする**

MODの設定画面に 「アーマーモデルのエクスポート」のボタンがあると思います。 このボタンを押すと、キャッシュ内のアルゴリズム生成結果がリソースパックとしてエクスポートされます。 生成されたリソースパックを適用することで、今後Minecraft 起動する度にアーマーデバッグモードをオンにする必要が無くなります。

![image](https://user-images.githubusercontent.com/79469058/168339170-1965ad10-eb2a-4ab4-919e-3f5d5b0480fd.png)
***
## **💡上記の方法でも不具合が解決しない場合、このような代替案もあります。**


デバッグモードを使用しても、鎧が正しく表示されない場合もあります。 これは、MODによって鎧をレンダリングする方法が様々であることが原因です。 そこで、簡易的ですがその鎧を表示させるための代替案を紹介します。

まずデフォルトのモデルを使用する必要があり、 その上で自分でアーマーモデルを作成していくことになります。

### assets/`modid`/animmodels/armor/`item_name.json`

item_name.json ファイルに下記のコードを入力して、アーマーのデフォルトモデルを適用します（modidには適用した鎧が含まれるmod名を、item_nameには適用したいアイテムのレジストリ名を設定してください）

```
{
    "parent": "epicfight:armor/model_name"
}
```
使用できるモデル名: `helmet_default, chestplate_default, leggings_default, boots_default`

次に、カスタムアーマーのテクスチャをデフォルトのモデルのテクスチャ形式に合わせるよう編集します。

![sample](https://user-images.githubusercontent.com/79469058/168444508-f1fb4ebe-5949-40ca-9015-7e920f1e6508.png)

_バニラアーマーモデルのテクスチャマップ（参考用）_

次にテクスチャを保存しますが、バニラモデルと混同する可能性があるため、既存のテクスチャを上書きしないように命名する必要があります。 代わりに、次のパスに編集したテクスチャを保存するようにしてください: assets/modid/`existing_path`/epicfight/`texturename` （例〔修正前〕: "assets/minecraft/textures/models/armor/iron_layer_1.png" 〔修正後〕"assets/minecraft/textures/models/armor/epicfight/iron_layer_1.png"）

## **💡 カスタムアーマーに透明度を設定する**
***

カスタムアーマーの中には、テクスチャに透明感があるものもあります。 これらのコードを追加することで、バトルモードで使用した際も透明にレンダリングされます。

```
{
    "render_properties": {
        "transparent": true
    },
        "vertices": {
                ...
        }
}
```