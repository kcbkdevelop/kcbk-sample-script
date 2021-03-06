# KCB改 サンプルスクリプト

KCB改で利用可能なスクリプトのサンプルです。

quest script に記載されているスクリプトはscripts/quest_state_user.txtにファイルを作成しそちらにコピーしてください。

それ以降のスクリプトは汎用出撃のイベントスクリプトのにコピーしてください。

出撃する艦の条件は特に実装していないので撃破回数は適当に調整してください。

例えば851,改装航空巡洋艦、出撃！は鈴谷改二が旗艦である必要がありますが、それは条件に加えていません。そのため鈴谷が旗艦でない場合でもカウントして達成と判断してしまいます。

851,改装航空巡洋艦、出撃！のquset scriptは以下のように5-1でＡ勝利以上１回、5-3でＡ勝利以上1回となっています。851の任務が有効な状態で鈴谷以外が旗艦で5-1でＡ勝利してもカウントしてしまいます。
```javascript
function quest_state_851(){
	if(
		count_win_rank_boss(5,1,0,"A",851)  >= 1
		&& count_win_rank_boss(5,3,0,"A",851)  >= 1
		)
	{
		return 1;
	}
	return 0;
}
```
その場合は以下のように5-1の判定を2以上にするなどして調整してください。
```javascript
function quest_state_851(){
	if(
		count_win_rank_boss(5,1,0,"A",851)  >= 2 //ここを2に変更する
		&& count_win_rank_boss(5,3,0,"A",851)  >= 1
		)
	{
		return 1;
	}
	return 0;
}
```

現在のカウントを知りたい場合は、汎用出撃のスクリプト編集画面で
```javascript
function is_enabled(){
	var cnt = count_win_rank_boss(5,1,0,"A",851);
	log("回数:" + cnt);
	return fasle;
}
```
のようにテスト実行をしてみてください。

なお、艦隊も条件に加えたscriptを作成したい場合はscripts/quest_state_battle.txtの249,「第五戦隊」出撃せよ！などの既存の定期任務を参考にしてください。
