<table border="2" bordercolor="green"><tbody><tr>  <td><p class="line891"><strong>Feature</strong> </p></td>
  <td><p class="line891"><strong>new test</strong> <tt>[[</tt> </p></td>
  <td><p class="line891"><strong>old test</strong> <tt>[</tt> </p></td>
  <td><p class="line891"><strong>Example</strong> </p></td>
</tr>
<tr>  <td colspan="1" rowspan="4" style="text-align: center"><span class="anchor" id="line-26"></span><p class="line862">string comparison </p></td>
  <td><p class="line891"><tt>&gt;</tt> </p></td>
  <td><p class="line891"><tt>\&gt;</tt> <a href="/BashFAQ/031#np">(*)</a> </p></td>
  <td><p class="line891"><tt>[[&nbsp;a&nbsp;&gt;&nbsp;b&nbsp;]]&nbsp;||&nbsp;echo&nbsp;"a&nbsp;does&nbsp;not&nbsp;come&nbsp;after&nbsp;b"</tt> </p></td>
</tr>
<tr>  <td><span class="anchor" id="line-27"></span><p class="line891"><tt>&lt;</tt> </p></td>
  <td><p class="line891"><tt>\&lt;</tt> <a href="/BashFAQ/031#np">(*)</a> </p></td>
  <td><p class="line891"><tt>[[&nbsp;az&nbsp;&lt;&nbsp;za&nbsp;]]&nbsp;&amp;&amp;&nbsp;echo&nbsp;"az&nbsp;comes&nbsp;before&nbsp;za"</tt> </p></td>
</tr>
<tr>  <td><span class="anchor" id="line-28"></span><p class="line891"><tt>=</tt> (or <tt>==</tt>) </p></td>
  <td><p class="line891"><tt>=</tt> </p></td>
  <td><p class="line891"><tt>[[&nbsp;a&nbsp;=&nbsp;a&nbsp;]]&nbsp;&amp;&amp;&nbsp;echo&nbsp;"a&nbsp;equals&nbsp;a"</tt> </p></td>
</tr>
<tr>  <td><span class="anchor" id="line-29"></span><p class="line891"><tt>!=</tt> </p></td>
  <td><p class="line891"><tt>!=</tt> </p></td>
  <td><p class="line891"><tt>[[&nbsp;a&nbsp;!=&nbsp;b&nbsp;]]&nbsp;&amp;&amp;&nbsp;echo&nbsp;"a&nbsp;is&nbsp;not&nbsp;equal&nbsp;to&nbsp;b"</tt> </p></td>
</tr>
<tr>  <td colspan="1" rowspan="6" style="text-align: center"><span class="anchor" id="line-30"></span><p class="line862">integer comparison </p></td>
  <td><p class="line891"><tt>-gt</tt> </p></td>
  <td><p class="line891"><tt>-gt</tt> </p></td>
  <td><p class="line891"><tt>[[&nbsp;5&nbsp;-gt&nbsp;10&nbsp;]]&nbsp;||&nbsp;echo&nbsp;"5&nbsp;is&nbsp;not&nbsp;bigger&nbsp;than&nbsp;10"</tt> </p></td>
</tr>
<tr>  <td><span class="anchor" id="line-31"></span><p class="line891"><tt>-lt</tt> </p></td>
  <td><p class="line891"><tt>-lt</tt> </p></td>
  <td><p class="line891"><tt>[[&nbsp;8&nbsp;-lt&nbsp;9&nbsp;]]&nbsp;&amp;&amp;&nbsp;echo&nbsp;"8&nbsp;is&nbsp;less&nbsp;than&nbsp;9"</tt> </p></td>
</tr>
<tr>  <td><span class="anchor" id="line-32"></span><p class="line891"><tt>-ge</tt> </p></td>
  <td><p class="line891"><tt>-ge</tt> </p></td>
  <td><p class="line891"><tt>[[&nbsp;3&nbsp;-ge&nbsp;3&nbsp;]]&nbsp;&amp;&amp;&nbsp;echo&nbsp;"3&nbsp;is&nbsp;greater&nbsp;than&nbsp;or&nbsp;equal&nbsp;to&nbsp;3"</tt> </p></td>
</tr>
<tr>  <td><span class="anchor" id="line-33"></span><p class="line891"><tt>-le</tt> </p></td>
  <td><p class="line891"><tt>-le</tt> </p></td>
  <td><p class="line891"><tt>[[&nbsp;3&nbsp;-le&nbsp;8&nbsp;]]&nbsp;&amp;&amp;&nbsp;echo&nbsp;"3&nbsp;is&nbsp;less&nbsp;than&nbsp;or&nbsp;equal&nbsp;to&nbsp;8"</tt> </p></td>
</tr>
<tr>  <td><span class="anchor" id="line-34"></span><p class="line891"><tt>-eq</tt> </p></td>
  <td><p class="line891"><tt>-eq</tt> </p></td>
  <td><p class="line891"><tt>[[&nbsp;5&nbsp;-eq&nbsp;05&nbsp;]]&nbsp;&amp;&amp;&nbsp;echo&nbsp;"5&nbsp;equals&nbsp;05"</tt> </p></td>
</tr>
<tr>  <td><span class="anchor" id="line-35"></span><p class="line891"><tt>-ne</tt> </p></td>
  <td><p class="line891"><tt>-ne</tt> </p></td>
  <td><p class="line891"><tt>[[&nbsp;6&nbsp;-ne&nbsp;20&nbsp;]]&nbsp;&amp;&amp;&nbsp;echo&nbsp;"6&nbsp;is&nbsp;not&nbsp;equal&nbsp;to&nbsp;20"</tt> </p></td>
</tr>
<tr>  <td colspan="1" rowspan="2" style="text-align: center"><span class="anchor" id="line-36"></span><p class="line862">conditional evaluation </p></td>
  <td><p class="line891"><tt>&amp;&amp;</tt> </p></td>
  <td><p class="line891"><tt>-a</tt> <a href="/BashFAQ/031#np2">(**)</a> </p></td>
  <td><p class="line891"><tt>[[&nbsp;-n&nbsp;$var&nbsp;&amp;&amp;&nbsp;-f&nbsp;$var&nbsp;]]&nbsp;&amp;&amp;&nbsp;echo&nbsp;"$var&nbsp;is&nbsp;a&nbsp;file"</tt> </p></td>
</tr>
<tr>  <td><span class="anchor" id="line-37"></span><p class="line891"><tt>||</tt> </p></td>
  <td><p class="line891"><tt>-o</tt> <a href="/BashFAQ/031#np2">(**)</a> </p></td>
  <td><p class="line891"><tt>[[&nbsp;-b&nbsp;$var&nbsp;||&nbsp;-c&nbsp;$var&nbsp;]]&nbsp;&amp;&amp;&nbsp;echo&nbsp;"$var&nbsp;is&nbsp;a&nbsp;device"</tt> </p></td>
</tr>
<tr>  <td><span class="anchor" id="line-38"></span><p class="line862">expression grouping </p></td>
  <td><p class="line891"><tt>(...)</tt> </p></td>
  <td><p class="line891"><tt>\(&nbsp;...&nbsp;\)</tt> <a href="/BashFAQ/031#np2">(**)</a> </p></td>
  <td><p class="line891"><tt>[[&nbsp;$var&nbsp;=&nbsp;img*&nbsp;&amp;&amp;&nbsp;($var&nbsp;=&nbsp;*.png&nbsp;||&nbsp;$var&nbsp;=&nbsp;*.jpg)&nbsp;]]&nbsp;&amp;&amp;</tt><br>
<tt>echo&nbsp;"$var&nbsp;starts&nbsp;with&nbsp;img&nbsp;and&nbsp;ends&nbsp;with&nbsp;.jpg&nbsp;or&nbsp;.png"</tt> </p></td>
</tr>
<tr>  <td><span class="anchor" id="line-39"></span><p class="line862">Pattern matching </p></td>
  <td><p class="line891"><tt>=</tt> (or <tt>==</tt>) </p></td>
  <td><p class="line862">(not available) </p></td>
  <td><p class="line891"><tt>[[&nbsp;$name&nbsp;=&nbsp;a*&nbsp;]]&nbsp;||&nbsp;echo&nbsp;"name&nbsp;does&nbsp;not&nbsp;start&nbsp;with&nbsp;an&nbsp;'a':&nbsp;$name"</tt> </p></td>
</tr>
<tr>  <td><span class="anchor" id="line-40"></span><p class="line891"><a href="/RegularExpression">RegularExpression</a> matching </p></td>
  <td><p class="line891"><tt>=~</tt> </p></td>
  <td><p class="line862">(not available) </p></td>
  <td><p class="line891"><tt>[[&nbsp;$(date)&nbsp;=~&nbsp;^Fri\&nbsp;...\&nbsp;13&nbsp;]]&nbsp;&amp;&amp;&nbsp;echo&nbsp;"It's&nbsp;Friday&nbsp;the&nbsp;13th!"</tt> </p></td>
</tr>
</tbody></table>
