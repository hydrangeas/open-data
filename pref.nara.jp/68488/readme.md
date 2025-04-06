# summary

## source

- breadcrumbs: 県民情報 > 県の組織 > 福祉保険部 > 医療政策局 > 地域医療連携課　医師・看護師確保対策室 > 保健衛生統計データ > 令和5年　確定数
- url: <https://www.pref.nara.jp/68488.htm>

## conversion steps

1. メタデータ用ファイルを作成する
   Excelのファイル名が `r5.xls` の場合、メタデータ用ファイル名は `r5.txt` とする（NotebookLMがjsonファイルのアップロードを許容しないため）。

   ```json
   {
     "metadata": {
       "title": "令和5年人口動態総覧（数・率）",
       "description": "令和5年人口動態総覧（数・率）",
       "category": "保健衛生統計",
       "source": {
         "url": "https://www.pref.nara.jp/secure/319985/r5.xls",
         "name": "r5.xls"
       },
       "license": {
         "type": "CC BY 4.0",
         "url": "https://creativecommons.org/licenses/by/4.0/",
         "licensor": "地域医療連携課",
         "issued": "2023-01-01T00:00:00+09:00"
       },
       "contact": {
         "organization": "奈良県",
         "department": "地域医療連携課",
         "tel": "0742-27-8653"
       },
       "created": "2025-04-01T00:00:00+09:00",
       "format": "Excel",
       "fileSize": "67KB",
       "updated": "2025-04-01T00:00:00+09:00"
     }
   }
   ```

   - title: Excelファイルのタイトル
   - description: Excelファイルのタイトル
   - category: breadcrumbsの一つ上をカテゴリとする
   - url: Excelファイルへのリンク
   - name: Excelファイル名
   - license: <https://www.pref.nara.jp/dd.aspx?menuid=46282> から引用
   - contact: <https://www.pref.nara.jp/dd.aspx?menuid=46282> から引用
   - created: 2025-04-01で固定
   - format: 今回はExcelファイルのみ
   - fileSize: タイトルに記載しているものを転記
   - updated: 2025-04-01で固定

2. Excelファイルを開き、PDFで保存する
3. NotebookLMに入れ、データ作成を依頼
   プロンプト例は以下の通り。

   ````text
   r5.pdfのすべてのdataをJSONに変換してください。
   また、r5.txtのmetadataとマージし、下記のフォーマットで出力してください。

   ```
   {
     data: {}
     metadata: {}
   }
   ```

   dataをJSONに変換する際は下記のルールを順守してください。

   - 意味的に無駄な空白は削除してください。例えば「市 計」は『市計』としてください。
   - 数値についてはすべてJSONでの数値として認識してください。例えば、「"７，１３３"」は『7133』としてください。
   - △はマイナスを表します。つまり、「"△３４２"」は『-342』としてください。
   - 数値が存在しない場合、"－", "-"は使わないでください（nullとして扱ってください）
   - value のすべてが null のオブジェクトについては削除してください

   出力は上記フォーマットのJSONのみとしてください。

   ````

## Notes

- 表7はr5-7.xlsと間違ってr5-6.xlsのリンクが置かれている（URL直叩きでアクセス可能）
- r5-14.xlsだけなぜかr5-14.zipに圧縮されている（圧縮ファイル内には他にファイルなし）

## Thoughts

- 出力されたkey名がかなり微妙なんだけど、プロンプトで指示するにしても結構コストが高かったので（色々失敗したので）後で考える
