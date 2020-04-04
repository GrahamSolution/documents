# テーブル定義書

## m_staff（社員マスタ）
|物理名|論理名|データ型|Not Null|桁数|デフォルト値|備考|
|---|---|---|---|---|---|---|
|staff_id|社員ID|int|yes(pk)||auto_increment|連番を自動採番する|
|mail_address|メールアドレス|varchar|yes|255||unique制約付き|
|login_id|ログインID|varchar|yes|255||unique制約付き|
|password|パスワード|varchar|yes|255|||
|create_at|作成日時|timestamp|yes||current_timestamp||
|update_at|更新日時|timestamp|yes||current_timestamp||

## m_staff_basic_info（社員基本情報マスタ）
|物理名|論理名|データ型|Not Null|桁数|デフォルト値|備考|
|---|---|---|---|---|---|---|
|staff_basic_info_id||int|yes(pk)||auto_increment|サロゲートキー|
|staff_id|社員ID|int|yes(fk)|||m_staffテーブルのpk|
|name|社員名|varchar||100|||
|name_kana|社員名（かな）|varchar||100|||
|entered_date|入社日|varchar||10|1900-01-01||
|birthday|誕生日|varchar||10|1900-01-01||
|telephone_number|電話番号|varchar||13|010-1234-5678||
|department_id|部署ID|int|yes(fk)|||m_departmentテーブルのpk|
|position_id|役職ID|int|yes(fk)|||m_positionテーブルのpk|
|grade_id|階級ID|int|yes(fk)|||m_gradeテーブルのpk|
|create_at|作成日時|timestamp|yes||current_timestamp||
|update_at|更新日時|timestamp|yes||current_timestamp||

## m_staff_detail_info（社員詳細情報マスタ：適当&いらないかも）
|物理名|論理名|データ型|Not Null|桁数|デフォルト値|備考|
|---|---|---|---|---|---|---|
|staff_detail_info_id||int|yes(pk)||auto_increment|サロゲートキー|
|staff_id|社員ID|int|yes(fk)|||m_staffテーブルのpk|
|hobby||varchar|趣味|255|||
|interest|興味のある仕事|varchar||255|||
|project_summary|案件概要|text|||||
|create_at|作成日時|timestamp|yes||current_timestamp||
|update_at|更新日時|timestamp|yes||current_timestamp||

## m_department（部署マスタ）
|物理名|論理名|データ型|Not Null|桁数|デフォルト値|備考|
|---|---|---|---|---|---|---|
|department_id|部署ID|int|yes(pk)||auto_increment|サロゲートキー|
|department_name|部署名称|varchar||50|||
|description|説明|text|||||
|create_at|作成日時|timestamp|yes||current_timestamp||
|update_at|更新日時|timestamp|yes||current_timestamp||

## m_position（役職マスタ）
|物理名|論理名|データ型|Not Null|桁数|デフォルト値|備考|
|---|---|---|---|---|---|---|
|position_id|役職ID|int|yes(pk)||auto_increment|サロゲートキー|
|position_name|役職名称|varchar||50|||
|create_at|作成日時|timestamp|yes||current_timestamp||
|update_at|更新日時|timestamp|yes||current_timestamp||

## m_grade（階級マスタ）
|物理名|論理名|データ型|Not Null|桁数|デフォルト値|備考|
|---|---|---|---|---|---|---|
|grade_id|階級ID|int|yes(pk)||auto_increment|サロゲートキー|
|grade_name|階級名称|varchar||50|||
|create_at|作成日時|timestamp|yes||current_timestamp||
|update_at|更新日時|timestamp|yes||current_timestamp||

## m_attendance（勤怠情報マスタ）
|物理名|論理名|データ型|Not Null|桁数|デフォルト値|備考|
|---|---|---|---|---|---|---|
|attendance_id||int|yes(pk)||auto_increment|サロゲートキー|
|staff_id|社員ID|int|yes(fk)|||m_staffテーブルのpk|
|year_month|年月|char|yes|6|190001|対象年月|
|customer_resident_time|客先勤務時間|decimal|yes|4, 2|0|客先勤務の場合は入力する|
|total_working_time|総労働時間|decimal|yes|4, 2|0||
|total_night_time|総深夜勤務時間|decimal|yes|4, 2|0||
|total_over_time|総残業時間|decimal|yes|4, 2|0||
|create_at|作成日時|timestamp|yes||current_timestamp||
|update_at|更新日時|timestamp|yes||current_timestamp||

## t_attendance（勤怠情報トランザクション）
|物理名|論理名|データ型|Not Null|桁数|デフォルト値|備考|
|---|---|---|---|---|---|---|
|attendance_id||int|yes(pk)||auto_increment|サロゲートキー|
|year_month|年月|char|yes|6|190001|対象年月|
|day|日付|char|yes|2|01|対象日付|
|staff_id|社員ID|int|yes(fk)|||m_staffテーブルのpk|
|start_time|始業時間|char||5|||
|end_time|終業時間|char||5|||
|rest_time|休憩時間|decimal|yes|4, 2|0||
|absence_type_id|欠勤種別|int||||1:欠勤、2:有給、3:代休、4:忌引|
|absence_reason|欠勤理由|varchar||255|||
|working_time|労働時間|decimal|yes|4, 2|||
|night_time|深夜勤務時間|decimal|yes|4, 2|||
|operating_expenses|営業費用|int|||0||
|section|営業区間|varchar||255|||
|remarks|備考|varchar||255|||
|create_at|作成日時|timestamp|yes||current_timestamp||
|update_at|更新日時|timestamp|yes||current_timestamp||

## m_attendance_setting（勤怠設定マスタ：APIとしては未使用）
|物理名|論理名|データ型|Not Null|桁数|デフォルト値|備考|
|---|---|---|---|---|---|---|
|attendance_setting_id||int|yes(pk)||auto_increment|サロゲートキー|
|staff_id|社員ID|int|yes(fk)|||m_staffテーブルのpk|
|home_nearest|自宅最寄り駅|varchar||100|||
|working_nearest|勤務地最寄り駅|varchar||100|||
|transportation_expenses|交通費|int|||0||
|working_place|勤務地|varchar||100|||
|regular_start_time|始業定時|char||5|09:00||
|regular_end_time|終業定時|char||5|17:30||
|create_at|作成日時|timestamp|yes||current_timestamp||
|update_at|更新日時|timestamp|yes||current_timestamp||

## m_role（権限マスタ）
|物理名|論理名|データ型|Not Null|桁数|デフォルト値|備考|
|---|---|---|---|---|---|---|
|role_id|権限ID|int|yes(pk)||auto_increment|サロゲートキー|
|role_name|権限名称|varchar|yes|255||ROLE_ADMIN, ROLE_MIDDLE, ROLE_USERの3種類の権限がある|
|create_at|作成日時|timestamp|yes||current_timestamp||
|update_at|更新日時|timestamp|yes||current_timestamp||

## c_staff_role（社員_権限連結）
|物理名|論理名|データ型|Not Null|桁数|デフォルト値|備考|
|---|---|---|---|---|---|---|
|staff_id|社員ID|int|yes(fk)|||m_staffテーブルのpk|
|role_id|権限ID|int|yes(fk)|||m_roleテーブルのpk|
|create_at|作成日時|timestamp|yes||current_timestamp||
|update_at|更新日時|timestamp|yes||current_timestamp||
