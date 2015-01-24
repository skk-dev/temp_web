#WEB版マニュアルの今後の運用について

| 問題・現象 | 原因・解決 | 手法 |
|------------|------------|------|
| WEB版マニュアル http://openlab.ring.gr.jp/skk/skk-manual/skk-manual-ja_10.html が文字化けしている。 | html の meta タグ charset=euc-jp が欠けている | sed で挿入 (cvswork.sh の修正) or <br> texi2html のバージョンアップ |
| 現在起動する texi2html は、中島さんのホームに置かれている 1.65 | 1.82 や 5.0 だと charset=utf-8 を挿入してくれる | nkf -e を廃止<br>下記のどれが適切か検討<br> texi2html-1.82<br> texi2html-5.0<br> makeinfo --html |
| 生成元である skk.texi が cvs 固定。web 公開領域に正しい html を置いても、そのうち cvs/skk.texi で上書きされてしまう | wget で github から取得 | cvswork.sh の修正 |
| cvswork.sh の修正が反映されない | CVSROOT/loginfo が起動しているのは、中島さんのホームに置かれている cvswork.sh | CVSROOT/loginfo の修正（中島さん版 cvswork.sh が起動しちゃうと上書きされてしまう） |
| 修正版 cvswork.sh の動作場所（中間ファイルが生じるため cvs 管理下はちょっと） | cvs commit が反映されること | `ln -s cvs/cvswork.sh /home/北本/cvswork.sh` |
| github へ移行したため、そもそも CVSROOT/loginfo が発動しない | cron で定期的に cvswork.sh を起動 | 許可が必要かも。当面は手動で起動 |
| そもそも、WEB版マニュアルの必要性 | 文字化けしたままでも良いのでは | 現状のまま（euc エンコードである旨の注意書きを追加） or<br>WEB版マニュアルの廃止 |
| texi2html-1.82/5.0 でも一部文字化け | info や html を生成できる他の手法 | org-mode |

##参考
* http://mail.ring.gr.jp/skk/201501/msg00073.html

* http://mail.ring.gr.jp/skk/201501/msg00074.html
