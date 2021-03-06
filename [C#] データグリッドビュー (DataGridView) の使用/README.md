# [C#] データグリッドビュー (DataGridView) の使用
## License
- Apache License, Version 2.0
## Technologies
- Visual Studio 2010
- .NET Framework 2.0
- Windows 7 Ultimate 64 bit
## Topics
- 逆引きサンプル コード
- Windows Form
## Updated
- 05/29/2011
## Description

<p>多くの業務アプリケーションでは必ずと言って良いほどデータのテーブル表示が要件に入ってきます。Windows フォームでは <a href="http://msdn.microsoft.com/ja-jp/library/system.windows.forms.datagridview" target="_blank">
DataGridView</a> コントロールが標準で用意されており、こちらを用いてデータのテーブル表示や操作を行うことが可能です。このコントロールではデータ ソースを設定してもしなくても行を表示することが可能です。また、テキスト表示以外にもリンク、画像、ボタンなど色々な表示が可能になっています。セルにボタンを配置し、クリック時に行を削除する方法は下記の通りです。なお、Windows フォーム アプリケーションの作成方法については
<a href="http://code.msdn.microsoft.com/C-Windows-dc42087f">[C#] Windows フォームによるクライアント アプリケーション開発</a>を参照してください。</p>
<h2 style="font-size:100%; font-weight:bold">1. Windows フォーム アプリケーション プロジェクトを作成し、フォームに DataGridView コントロールを追加します。</h2>
<p><img src="18596-image001.jpg" alt="図 1" width="600" height="356"></p>
<h2 style="font-size:100%; font-weight:bold">2. コントロール右上のスマート タグから [列の追加...] を選択し、列の追加ウイザードを表示させます。</h2>
<p><img src="18103-image002.jpg" alt="図 2" width="600" height="375"></p>
<h2 style="font-size:100%; font-weight:bold">3. 非バインドの列を下記のように追加します。</h2>
<table class="grid" border="1" cellspacing="0" cellpadding="5" style="border-collapse:collapse; margin-bottom:10px">
<tbody>
<tr style="background-color:#eff3f7">
<td valign="top"><strong>名前</strong></td>
<td valign="top"><strong>型</strong></td>
<td valign="top"><strong>ヘッダー テキスト</strong></td>
</tr>
<tr>
<td valign="top"><strong>DelBtn</strong></td>
<td valign="top">DataGridViewButtonColumn</td>
<td valign="top">削除</td>
</tr>
<tr>
<td valign="top"><strong>PersonName</strong></td>
<td valign="top">DataGridViewTextColumn</td>
<td valign="top">名前</td>
</tr>
<tr>
<td valign="top"><strong>Age</strong></td>
<td valign="top">DataGridViewTextColumn</td>
<td valign="top">年齢</td>
</tr>
</tbody>
</table>
<p><img src="18104-image003.jpg" alt="図 3" width="486" height="513"></p>
<p>Form1.cs を開き、コードで行のデータを追加します。最初の文字列がグリッド セルのボタンに表示されます。</p>
<div class="scriptcode">
<div class="pluginEditHolder" pluginCommand="mceScriptCode">
<div class="title">C#</div>
<div class="pluginEditHolderLink">スクリプトの編集</div>
<span class="hidden">csharp</span>

<pre id="codePreview" class="csharp"><span class="cs__keyword">public</span>&nbsp;Form1()&nbsp;<br>{&nbsp;<br>&nbsp;&nbsp;&nbsp;&nbsp;InitializeComponent();&nbsp;<br>&nbsp;<br>&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;DataGridView&nbsp;にデータを追加</span>&nbsp;<br>&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">this</span>.dataGridView1.Rows.Add(<span class="cs__string">&quot;削除&quot;</span>,&nbsp;<span class="cs__string">&quot;山田　太郎&quot;</span>,&nbsp;<span class="cs__number">28</span>);&nbsp;<br>&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">this</span>.dataGridView1.Rows.Add(<span class="cs__string">&quot;削除&quot;</span>,&nbsp;<span class="cs__string">&quot;鈴木　衛&quot;</span>,&nbsp;<span class="cs__number">47</span>);&nbsp;<br>&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">this</span>.dataGridView1.Rows.Add(<span class="cs__string">&quot;削除&quot;</span>,&nbsp;<span class="cs__string">&quot;斉藤　花子&quot;</span>,&nbsp;<span class="cs__number">32</span>);&nbsp;<br>&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">this</span>.dataGridView1.Rows.Add(<span class="cs__string">&quot;削除&quot;</span>,&nbsp;<span class="cs__string">&quot;田中　美恵&quot;</span>,&nbsp;<span class="cs__number">50</span>);&nbsp;<br>}&nbsp;<br>&nbsp;<br></pre>
</div>
</div>
<h2 style="font-size:100%; font-weight:bold">4. デザイン 画面に戻り、DataGridView のCellContentClick イベントにイベント ハンドラーを設定します。</h2>
<p><img src="18105-image004.jpg" alt="図 4" width="600" height="365"></p>
<p>このイベントはセル内部のコンテンツをクリックした際にイベントが発生するため、イベント引数からボタン列であるかを判定し、更に削除確認を行います。OK ボタンが押された場合に行を削除します。</p>
<div class="scriptcode">
<div class="pluginEditHolder" pluginCommand="mceScriptCode">
<div class="title">C#</div>
<div class="pluginEditHolderLink">スクリプトの編集</div>
<span class="hidden">csharp</span>

<pre id="codePreview" class="csharp"><span class="cs__keyword">private</span>&nbsp;<span class="cs__keyword">void</span>&nbsp;dataGridView1_CellContentClick(<span class="cs__keyword">object</span>&nbsp;sender,&nbsp;DataGridViewCellEventArgs&nbsp;e)&nbsp;<br>{&nbsp;<br>&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;削除ボタン列かどうかを確認</span>&nbsp;<br>&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">if</span>&nbsp;(e.ColumnIndex&nbsp;==&nbsp;<span class="cs__keyword">this</span>.dataGridView1.Columns[<span class="cs__string">&quot;DelBtn&quot;</span>].Index)&nbsp;<br>&nbsp;&nbsp;&nbsp;&nbsp;{&nbsp;<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">if</span>&nbsp;(DialogResult.Yes&nbsp;==&nbsp;MessageBox.Show(<span class="cs__string">&quot;削除しますか&quot;</span>,&nbsp;<span class="cs__string">&quot;確認&quot;</span>,&nbsp;&nbsp;<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;MessageBoxButtons.YesNo,&nbsp;&nbsp;MessageBoxIcon.Question))&nbsp;<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{&nbsp;<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;削除</span>&nbsp;<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">this</span>.dataGridView1.Rows.RemoveAt(e.RowIndex);&nbsp;<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;<br>&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;<br>}&nbsp;<br>&nbsp;<br></pre>
</div>
</div>
<p>実行結果は下記の通りです。</p>
<p><img src="18106-image005.jpg" alt="図 5" width="300" height="300"></p>
<p>削除列にボタンが表示されテーブルが表示されます。削除ボタンをクリックすると確認ダイアログが開きます。</p>
<p><img src="18107-image006.jpg" alt="図 6" width="480" height="377"></p>
<p>OK をクリックすることで行が削除されます。</p>
<p><img src="18108-image007.jpg" alt="図 7" width="300" height="300"></p>
<p>今回は DataGridView にデータをコードで作成し、行削除を実行しました。DataGridView ではこのほか色々な機能を持っています。例として、偶数行の表示を設定する方法については
<a href="http://beta.code.msdn.microsoft.com/10-Grid-C-509464bc">10 行でズバリ !! 複合 Grid の作成 (C#)</a> に記載がありますので確認してみてください。</p>
<h2 style="margin-top:30px">関連リンク</h2>
<ul>
<li><a href="http://msdn.microsoft.com/ja-jp/library/system.windows.forms.datagridview" target="_blank">DataGridView クラス</a>
</li><li><a href="http://beta.code.msdn.microsoft.com/10-Grid-C-509464bc">10 行でズバリ!! 複合 Grid の作成 (C#)</a>
</li></ul>
<hr style="clear:both; margin-bottom:8px; margin-top:20px">
<table>
<tbody>
<tr>
<td><a href="http://msdn.microsoft.com/ja-jp/samplecode.recipe"><img src="http://i.msdn.microsoft.com/ff950935.coderecipe_180x70%28ja-jp,MSDN.10%29.jpg" border="0" alt="Code Recipe" width="180" height="70" style="margin-top:3px"></a></td>
<td><a href="http://msdn.microsoft.com/ja-jp/windows/" target="_blank"><img src="http://i.msdn.microsoft.com/ff950935.windows_180x70%28ja-jp,MSDN.10%29.jpg" border="0" alt="Windows デベロッパー センター" width="180" height="70" style="margin-top:3px"></a></td>
<td>
<ul>
<li>もっと他のコンテンツを見る &gt;&gt; <a href="http://msdn.microsoft.com/ja-jp/ff363212" target="_blank">
逆引きサンプル コード一覧へ</a> </li><li>もっと他のレシピを見る &gt;&gt; <a href="http://msdn.microsoft.com/ja-jp/samplecode.recipe">
Code Recipe へ</a> </li><li>もっと Windows の情報を見る &gt;&gt; <a href="http://msdn.microsoft.com/ja-jp/windows/" target="_blank">
Windows デベロッパー センターへ</a> </li></ul>
</td>
</tr>
</tbody>
</table>
<p style="margin-top:20px"><a href="#top"><img src="http://www.microsoft.com/japan/msdn/nodehomes/graphics/top.gif" border="0" alt="">ページのトップへ</a></p>
