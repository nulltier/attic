# Rust by My Own Example

<table style="float: left"><thead>
    <th>Task</th>
    <th>Solution</th>
</thead><tbody>

<tr style="vertical-align: top;"><td>
Encode a string to URL
</td><td>

There is no dedicated method implemented within `std`, rely on the crates. Consider
[urlencoding](https://crates.io/crates/urlencoding) and
[utl](https://crates.io/crates/url), for example.

They both are doing encoding on the binary data representation with relying on the 
[URL spec](https://url.spec.whatwg.org/).

Do no see any practical use of any attempts to implemen this logic on the application level.  

<pre><code class="language-rust">
use urlencoding::encode;

let input = "https://music.yandex.ru/album/2459398/track/21484345";
println!("{}", urlencoding::encode(input)); 
// https%3A%2F%2Fmusic.yandex.ru%2Falbum%2F2459398%2Ftrack%2F21484345
</code></pre>
</td></tr>

</tbody></table>
