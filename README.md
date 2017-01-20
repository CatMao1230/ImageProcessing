# ImageProcessing
<h1><img class="alignnone  wp-image-99" src="https://catmaoblog.files.wordpress.com/2016/10/6lqz4de.png" alt="Icon made by Freepik from www.flaticon.com" width="40" height="40" /> <a href="https://catmao1230.github.io/ImageProcessing/" target="_blank">點我前往</a>
<h1><img class="alignnone  wp-image-99" src="https://catmaoblog.files.wordpress.com/2016/10/6lqz4de.png" alt="Icon made by Freepik from www.flaticon.com" width="40" height="40" /> <a href="https://catmaoblog.wordpress.com/2016/11/14/imageprocessing/" target="_blank">WordPress</a>
<h1><img class="alignnone  wp-image-41" src="https://catmaoblog.files.wordpress.com/2016/10/3h9rzur.png" alt="Icon made by Popcorns Arts from www.flaticon.com" width="40" height="40" /> 前言</h1>
「網際網路程式設計」<a href="http://blog.xuite.net/wen_pinn/blog" target="_blank">方老師</a>最近教我們使用 Javascript 來達到影像處理的功能，使用 <a href="http://www.w3school.com.cn/tags/canvas_getimagedata.asp" target="_blank">GetImageData()</a> 來取得圖像的 RGB 值，加以改變便可使影像變化。本次作業是做一個美肌的影像處理，可以用 if 來搜尋所有的皮膚色，將九宮格內的皮膚色加以平均，如此一來便達到美膚的效果。

以下圖檔可以下載以測試美膚的效果：

<img class="alignnone size-full wp-image-537" src="https://catmaoblog.files.wordpress.com/2016/11/6awg8kr.jpg" alt="6awg8kr" width="328" height="471" />
<h1><img class="alignnone  wp-image-43" src="https://catmaoblog.files.wordpress.com/2016/10/ril6i6c.png" alt="Icon made by flaticon from www.flaticon.com" width="40" height="40" /> 程式碼</h1>
此網頁共有兩個 canvas ，左為原圖，右為影像處理後的圖像，方便看出其差異性。以下一一解說各按鈕功能及其原理。
<ul>
	<li><strong> Original</strong>
將圖像還原為原圖。</li>
	<li><strong> Inverse
</strong><img class="alignnone size-full wp-image-538" src="https://catmaoblog.files.wordpress.com/2016/11/ckpvjdo.png" alt="ckpvjdo" width="838" height="601" />
反轉圖像每個像素的顏色。255 - 原本的值就會是反轉後的顏色。在 <a href="http://www.w3school.com.cn/tags/canvas_getimagedata.asp" target="_blank">GetImageData()</a> 的最下方範例就有這個實例。
<pre><code>for (var i = 0; i < imgData.data.length; i+=4)
{
    imgData.data[i]   = 255 - imgData.data[i];
    imgData.data[i+1] = 255 - imgData.data[i+1];
    imgData.data[i+2] = 255 - imgData.data[i+2];
    imgData.data[i+3] = 255;
}</code></pre>
</li>
	<li><strong>Channel</strong>
<img class="alignnone size-full wp-image-539" src="https://catmaoblog.files.wordpress.com/2016/11/v7p824c.png" alt="v7p824c" width="838" height="601" />
將圖像分成上中下三塊，並分層顯示顏色，第一層只顯示紅色，第二層只顯示綠色，第三層只顯示藍色。以第一層紅色為例，保留 R 的值，其餘改為 0 ，不透明度維持 255 ：
<pre><code>for (var i = 0; i < DesData.data.length / 3; i+=4) // 除以 3 是因為分成三層
{
    DesData.data[i]   = DesData.data[i];
    DesData.data[i+1] = 0;
    DesData.data[i+2] = 0;
    DesData.data[i+3] = 255;
}</code></pre>
</li>
	<li><strong>ChannelRed
<img class="alignnone size-full wp-image-541" src="https://catmaoblog.files.wordpress.com/2016/11/xlfjzch.png" alt="xlfjzch" width="838" height="601" />
</strong>全圖只保留 R 的值。</li>
	<li><strong>ChannelGreen
<img class="alignnone size-full wp-image-542" src="https://catmaoblog.files.wordpress.com/2016/11/grcsdjt.png" alt="grcsdjt" width="838" height="601" />
</strong>全圖只保留 G 的值。</li>
	<li><strong>ChannelBlue
<img class="alignnone size-full wp-image-543" src="https://catmaoblog.files.wordpress.com/2016/11/fuakzhi.png" alt="fuakzhi" width="838" height="601" />
</strong>全圖只保留 B 的值。</li>
	<li><strong>Red</strong>
<img class="alignnone size-full wp-image-545" src="https://catmaoblog.files.wordpress.com/2016/11/xlpqrxm.png" alt="xlpqrxm" width="838" height="601" />
全圖變更紅， R 的值會變為原先的兩倍，而其餘則為原先的一半。
<pre><code>for (var i = 0; i < DesData.data.length; i+=4)
{
    DesData.data[i]   = Math.min(255, DesData.data[i] * 2); // 若 R 值的兩倍超出 255 則為 255 
    DesData.data[i+1] = DesData.data[i+1] / 2;
    DesData.data[i+2] = DesData.data[i+2] / 2;
    DesData.data[i+3] = 255;
}</code></pre>
</li>
	<li><b>Green</b>
<img class="alignnone size-full wp-image-546" src="https://catmaoblog.files.wordpress.com/2016/11/epfpktx.png" alt="epfpktx" width="838" height="601" />
全圖變更綠， G 的值會變為原先的兩倍，而其餘則為原先的一半。</li>
	<li><b>Blue</b>
<img class="alignnone size-full wp-image-547" src="https://catmaoblog.files.wordpress.com/2016/11/r91eyss.png" alt="r91eyss" width="838" height="601" />
全圖變更藍， B 的值會變為原先的兩倍，而其餘則為原先的一半。</li>
	<li><strong>Gray
<img class="alignnone size-full wp-image-548" src="https://catmaoblog.files.wordpress.com/2016/11/cfcwk1p.png" alt="cfcwk1p" width="838" height="601" /></strong>
將全圖變成灰色。人的肉眼看得灰色並不是 RGB 加總除以 3 ，而是有既定的公式。有人將此值測出來為：0.2126 * R + 0.7152 * G + 0.0722 * B 。因此將 RGB 都套用公式即可變成灰色的圖片。
<pre><code>for (var i = 0; i < DesData.data.length; i+=4)
{
    avg = 0.2126 * DesData.data[i]
        + 0.7152 * DesData.data[i+1]
        + 0.0722 * DesData.data[i+2];
    DesData.data[i]   = avg;
    DesData.data[i+1] = avg;
    DesData.data[i+2] = avg;
    DesData.data[i+3] = DesData.data[i+3];
}</code></pre>
</li>
	<li><strong>Binary</strong>
<img class="alignnone size-full wp-image-549" src="https://catmaoblog.files.wordpress.com/2016/11/t3qz3mk.png" alt="t3qz3mk" width="838" height="601" />
將圖片二值化，非 255 即 0 ，若該 Gray 之後的 avg 值大於 128 為 255 ，否則為 0 。
<pre><code>for (var i = 0; i < DesData.data.length; i+=4) {
    avg = 0.2126 * DesData.data[i]
        + 0.7152 * DesData.data[i+1]
        + 0.0722 * DesData.data[i+2];
    DesData.data[i]   = avg > 128 ? 255 : 0;
    DesData.data[i+1] = avg > 128 ? 255 : 0;
    DesData.data[i+2] = avg > 128 ? 255 : 0;
    DesData.data[i+3] = 255;
}</code></pre>
</li>
	<li><strong>SkinToGray</strong>
<img class="alignnone size-full wp-image-550" src="https://catmaoblog.files.wordpress.com/2016/11/iruulty.png" alt="iruulty" width="838" height="601" />
將皮膚色的區域改為灰色。先找出最大和最小的 RGB 值，再利用以下 if 判斷是判斷是否為皮膚色： R > 95 && G > 40 && B > 20 && ( max - min ) > 15 && Math.abs( R - G ) > 15 && R > G && R > B 。 Max() 和 Min() 是我自己寫的函式，用來取最大與最小值。
<pre><code>for (var i = 0; i < DesData.data.length; i+=4) {
    avg = 0.2126 * DesData.data[i]
        + 0.7152 * DesData.data[i+1]
        + 0.0722 * DesData.data[i+2];
  
    var max = Max(DesData.data[i], DesData.data[i+1], DesData.data[i+2]);
    var min = Min(DesData.data[i], DesData.data[i+1], DesData.data[i+2]);

    if(DesData.data[i] > 95 && DesData.data[i+1] > 40 && DesData.data[i+2] > 20 && (max - min) > 15 && Math.abs(DesData.data[i] - DesData.data[i+1]) > 15 && DesData.data[i] > DesData.data[i+1] && DesData.data[i] > DesData.data[i+2])
    {
        DesData.data[i]   = avg;
        DesData.data[i+1] = avg;
        DesData.data[i+2] = avg;
    }
}</code></pre>
</li>
	<li><strong>Skin</strong>
<img class="alignnone size-full wp-image-551" src="https://catmaoblog.files.wordpress.com/2016/11/neoxp0j.png" alt="neoxp0j" width="838" height="601" />
美化皮膚，將皮膚色的區域做模糊。
arrSkin[] 用來存放是否為皮膚色，將整張圖掃過後，皮膚色為 True ，其餘則為 False 。再度掃過整張圖片，若為皮膚色，則探訪其周圍的九宮格是否也為皮膚色，若都為皮膚色則做平均，將平均值放入此格。
nine[] 用來存放九宮格的位置。如下圖所示， w 為 canvas 的寬度， imgData 存放著 RGBA 值，所以九宮格的位置差需要乘以 4 才是 imgData 的值：
<img class="alignnone size-full wp-image-552" src="https://catmaoblog.files.wordpress.com/2016/11/xki6itl.png" alt="xki6itl" width="484" height="488" />
<pre><code>var nine = [i-(w-1)*4, i-w*4, i-(w+1)*4, i-4, i, i+4, i+(w-1)*4, i+w*4, i+(w+1)*4];</code></pre>
</li>
</ul>
<h1><img class="alignnone  wp-image-42" src="https://catmaoblog.files.wordpress.com/2016/10/tpodion.png" alt="tpodion" width="40" height="40" /> 參考資料</h1>
<ul class="alt">
	<li><a href="http://www.csie.ntnu.edu.tw/~u91029/Image.html" target="_blank">Image / 演算法筆記</a></li>
	<li><a href="http://blog.xuite.net/wen_pinn/blog" target="_blank">新充滿奇蹟的寶寶 / 方文聘老師</a></li>
</ul>
