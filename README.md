```sql
select genre_romantrans, remywiki_title, artist from songs where genre_romantrans like 'hyper%';
```
|  genre_romantrans  |       remywiki_title        |       artist       |
|--------------------|-----------------------------|--------------------|
| HYPER J-POP        | STARS                       | TЁЯRA              |
| HYPER J-POP 2      | North Wind                  | TЁЯRA              |
| HYPER J-POP 3      | 1/6billionth                | TЁЯRA              |
| HYPER EUROBEAT     | KISS KISS KISS              | NAOKI feat. SHANTI |
| HYPER J-ROCK       | Brave!                      | TЁЯRA              |
| HYPER JAPANESQUE   | Mugen no hikari             | TЁЯRA              |
| HYPER MASQUERADE   | Masquerade                  | TЁЯRA              |
| HYPER CHINESE POP  | Toukarenjou                 | TЁЯRA              |
| HYPER J-PARTY ROCK | MIRACLE FLYER!!             | TЁЯRA              |
| HYPER JAPANESQUE 2 | Hana ranman -Flowers-       | TЁЯRA              |
| HYPER FANTASIA     | Fantasia                    | TЁЯRA              |
| HYPER JAPANESQUE 3 | Tenjou no hoshi ~reimeiki~  | TЁЯRA              |
| HYPER DRAMATIC     | Bara wa towa ni utsukushiku | TЁЯRA              |
| HYPER JAPANESQUE   | Mugen no hikari             | TЁЯRA              |
| HYPER CHINESE POP  | Toukarenjou                 | TЁЯRA              |

```sql
select c.difficulty, c.level, s.remywiki_title, s.artist, h.rating from charts c join songs s on c.song_id = s.id join hyrorre_charts h on c.hyrorre_page_path = h.page_path where s.artist like '%dj taka%' and c.level >= 42 and c.level <= 45 order by c.level, c.difficulty;
```
| difficulty | level |   remywiki_title   |                       artist                       |    rating     |
|------------|-------|--------------------|----------------------------------------------------|---------------|
| h          | 42    | True Blue          | dj TAKA feat.AiMEE                                 | 強(+0.594±0.4) |
| h          | 42    | Triple Counter     | DJ YOSHITAKA meets dj TAKA                         | 弱(-0.706±0.5) |
| ex         | 43    | Memories (TAKA)    | dj TAKA                                            | 中(+0.118±0.4) |
| h          | 43    | Trill auf G        | BEMANI Sound Team "dj TAKA"                        | 中(+0.059±0.7) |
| h          | 43    | Triple Cross       | BEMANI Sound Team "dj TAKA & DJ YOSHITAKA & SYUNN" |               |
| ex         | 44    | LOVE2 Sugar        | dj TAKA feat.のりあ                                   | 中(-0.391±0.6) |
| h          | 44    | Elemental Creation | dj TAKA meets DJ YOSHITAKA                         | 強(+0.470±0.5) |
| ex         | 45    | Shock Me           | dj TAKA feat.Fuuuːka                               | 弱(-0.530±0.5) |
