```sql
select genre_romantrans, remywiki_title, artist
from songs
where genre_romantrans like 'hyper%';
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
select level, count(*) charts
from charts
where level >= 35
group by level;
```
| level | charts |
|-------|--------|
| 35    | 107    |
| 36    | 144    |
| 37    | 167    |
| 38    | 222    |
| 39    | 192    |
| 40    | 231    |
| 41    | 229    |
| 42    | 229    |
| 43    | 200    |
| 44    | 178    |
| 45    | 195    |
| 46    | 215    |
| 47    | 189    |
| 48    | 122    |
| 49    | 69     |
| 50    | 20     |



```sql
with l as (select * from labels where record_type = 'song' and value = 'upper')
select genre_romantrans, count(*) count
from songs s
left join l on s.id = l.record_id
where l.record_id is null -- exclude uppers since they're duplicates
group by genre_romantrans
having count > 1
order by count desc, genre_romantrans;
```
| genre_romantrans | count |
|------------------|-------|
| HAPPY HARDCORE   | 6     |
| PROGRESSIVE      | 3     |
| TECHNO POP       | 3     |
| ANTHEM           | 2     |
| BEAT ROCK        | 2     |
| CANDY POP        | 2     |
| CANDY RAVE       | 2     |
| EUROBEAT         | 2     |
| FUNK ROCK        | 2     |
| GIRLS ROCK       | 2     |
| HIPHOP           | 2     |
| INFINITY         | 2     |
| J-POP            | 2     |
| J-R&B            | 2     |
| LOUNGE POP       | 2     |
| MIXTURE          | 2     |
| PROGRE           | 2     |
| PUNK             | 2     |
| SKA              | 2     |
| TRANCE           | 2     |
| TRIBAL           | 2     |
| VISUAL           | 2     |
| Xmas PRESENTS    | 2     |



```sql
select distinct s.remywiki_title, s.genre_romantrans, h.duration
from charts c
join songs s on c.song_id = s.id
join hyrorre_charts h on c.hyrorre_page_path = h.page_path
order by h.duration_sec desc
limit 15;
```
|               remywiki_title                |              genre_romantrans               | duration |
|---------------------------------------------|---------------------------------------------|----------|
| Help me, ERINNNNNN!! -VENUS mix-            | Help me, ERINNNNNN!! -VENUS mix-            | 2:39     |
| Pop'n Xmas 2004 ~denshi no utagoe~          | Xmas PRESENTS                               | 2:33     |
| SDVX REMIX SELECTION for pop'n music vol.01 | SDVX REMIX SELECTION for pop'n music vol.01 | 2:33     |
| HYMN                                        | HYMN                                        | 2:31     |
| Sayonara no uta                             | Sayonara no uta                             | 2:30     |
| Homesick Pt.2&3                             | SOFT ROCK LONG                              | 2:26     |
| DDR MEGAMIX                                 | DDR                                         | 2:26     |
| Un Happy Heart                              | Un Happy Heart                              | 2:25     |
| Pop'n Xmas 2004 ~denshi no utagoe~          | Xmas PRESENTS                               | 2:24     |
| Romance (Kazuyoshi Maruyama)                | LATIN ENKA                                  | 2:22     |
| Neu                                         | NIENTE                                      | 2:21     |
| Ongaku                                      | SILENT                                      | 2:21     |
| Kouen(Live Version)                         | Kouen(Live Version)                         | 2:20     |
| Tsukiyuki ni mau hana no youni              | FOREST SNOW                                 | 2:19     |
| NAMINORI www.                               | LOUD BEACH                                  | 2:19     |



```sql
select round(cast(h.notes as real) / h.duration_sec, 3) nps, h.notes, h.duration, s.remywiki_title, s.genre_romantrans, c.difficulty diff, c.level
from charts c
join songs s on c.song_id = s.id
join hyrorre_charts h on c.hyrorre_page_path = h.page_path
where h.notes is not null
and h.duration_sec is not null
and c.level >= 46
order by nps
limit 10;
```
|  nps  | notes | duration |     remywiki_title      | genre_romantrans  | diff | level |
|-------|-------|----------|-------------------------|-------------------|------|-------|
| 5.802 | 528   | 1:31     | Maritare!               | CLASSIC 6         | ex   | 47    |
| 5.82  | 518   | 1:29     | GALAXY FOREST 11.6&12   | SCREEN            | h    | 46    |
| 6.269 | 746   | 1:59     | Doll's sight            | CLASSIC 10        | ex   | 48    |
| 6.669 | 807   | 2:01     | Hell? or Heaven?        | CLASSIC 9         | ex   | 49    |
| 7.06  | 826   | 1:57     | Eien toiu na no biyaku  | PYRAMID           | ex   | 47    |
| 7.112 | 633   | 1:29     | GALAXY FOREST 11.6&12   | SCREEN            | ex   | 49    |
| 7.308 | 782   | 1:47     | Nishiazabu suidou kyoku | PERCUSSIVE 2      | ex   | 46    |
| 7.716 | 1034  | 2:14     | Popperz Chronicle       | Popperz Chronicle | h    | 46    |
| 7.85  | 942   | 2:00     | School Life             | KESHIGOMU         | ex   | 46    |
| 7.958 | 955   | 2:00     | Omoide wo arigatou      | CLASSIC 11        | ex   | 49    |

```sql
...
order by nps desc
limit 10;
```
|  nps   | notes | duration |      remywiki_title       |   genre_romantrans   | diff | level |
|--------|-------|----------|---------------------------|----------------------|------|-------|
| 16.091 | 1947  | 2:01     | Oto                       | Oto                  | ex   | 50    |
| 16.037 | 1748  | 1:49     | Schrodinger no neko       | TOY CONTEMPORARY     | ex   | 50    |
| 15.517 | 1800  | 1:56     | ShinchoushinTION          | COREDUST BEAT        | ex   | 50    |
| 14.964 | 1646  | 1:50     | MADSPEED kyoushintou      | MADSPEED kyoushintou | ex   | 49    |
| 14.785 | 1789  | 2:01     | 25 o'clock the WORLD      | 25 o'clock the WORLD | ex   | 50    |
| 14.742 | 1769  | 2:00     | Seimei no honoo matoite   | IMBOLC               | ex   | 50    |
| 14.472 | 1780  | 2:03     | Shounen wa sora wo tadoru | MURAKUMO             | ex   | 50    |
| 14.394 | 1828  | 2:07     | Tadoru kimi wo koete      | Tadoru kimi wo koete | ex   | 50    |
| 14.387 | 1525  | 1:46     | Shuumatsu wo ou mono      | JUDGMENT             | ex   | 49    |
| 14.294 | 1458  | 1:42     | Kodomo live               | WARABE STEP          | ex   | 48    |
