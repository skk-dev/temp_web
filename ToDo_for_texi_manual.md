#WEB版マニュアルの今後の運用について

| 問題・現象 | 原因・解決 | 手法 |
|------------|------------|------|
| WEB版マニュアル http://openlab.ring.gr.jp/skk/skk-manual/skk-manual-ja_10.html が文字化けしている。 | texi を utf-8 のまま用いる | GNU texinfo 5.2 を使うことで対応 <br> texi2any --html --set-customization-variable FRAMES=1 skk.texi |
| 現在起動する texi2html は、中島さんのホームに置かれている 1.65 | 北本さんコンパイルの texinfo で対応する | nkf は使用しない <br> cvswork.sh の修正は未 |
| 生成元である skk.texi が cvs 固定。web 公開領域に正しい html を置いても、そのうち cvs/skk.texi で上書きされてしまう | wget で github から取得 | cvswork.sh の修正(未) <br> とりあえずは github と非同期に手動で更新 |
| 修正版 cvswork.sh の動作場所（中間ファイルが生じるため cvs 管理下はちょっと） | cvs commit が反映されること | `ln -s cvs/cvswork.sh /home/北本/cvswork.sh` |
| github へ移行したため、そもそも CVSROOT/loginfo が発動しない | cron で定期的に cvswork.sh を起動<br> 当面は手動で起動 | 許可が必要かも。 http://www.jp.freebsd.org/cgi/mroff.cgi?sect=1&cmd=&lc=1&subdir=man&dir=jpman-5.2.0%2Fman&subdir=man&man=crontab より、ユーザ用のcrontab を生成した後に cron を実行することで定期運用が可能と思われる。 https://mail.google.com/mail/u/0/#inbox/14b1cf427072b2fd |
| そもそも、WEB版マニュアルの必要性 | 当面は手動でgithubと同期 | 将来的にはorg-modeへの移行やWEB版マニュアルの廃止も含めて要検討 |

##参考
* http://mail.ring.gr.jp/skk/201501/msg00073.html

* http://mail.ring.gr.jp/skk/201501/msg00074.html

* http://mail.ring.gr.jp/skk/201502/msg00000.html
