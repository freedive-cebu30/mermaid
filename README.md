# mermaid

erDiagram
  administrators {
    INTEGER id PK "ID"
    INTEGER dealer_id "販売店ID(代理店用)"
    INTEGER project_id "プロジェクトID(店舗管理オーナー用)"
    VARCHAR name "管理者名"
    ENUM type "アカウントタイプ"
    VARCHAR email "管理者のメールアドレス"
    VARCHAR password "パスワード（ハッシュ化）"
    TINYINT is_active "アクティブフラグ（true:有効, false:無効）"
    DATETIME last_logged_in_at "最終ログイン日時"
    TIMESTAMP created_at "作成日時"
    TIMESTAMP updated_at "更新日時"
    TIMESTAMP deleted_at
  }
  advertisements {
    INTEGER id PK "ID"
    INTEGER shop_id FK "ショップID"
    VARCHAR name "広告名"
    VARCHAR external_url "外部URL"
    ENUM type "広告タイプ"
    ENUM file_format "ファイル形式"
    VARCHAR qr_file_path "QRファイルパス"
    VARCHAR short_url_path "短縮URLパス"
    INTEGER count "表示回数"
    TIMESTAMP created_at "作成日時"
    TIMESTAMP updated_at "更新日時"
  }
  analysis_reports {
    INTEGER id PK "ID"
    VARCHAR name "分析名"
    ENUM category "measure_proposals:試作提案,store_analysis:店舗分析,step_scenarios:ステップシナリオ,\n sns_posts:SNS投稿文,message_drafts:メッセージ文案,review_requests:レビュー依頼文,\n persona_design:ペルソナ設計,o"
    ENUM status "処理状態"
    TEXT output "出力内容"
    DATETIME completed_at "完了日時"
    DATETIME failed_at "失敗日時"
    INTEGER shop_id FK "店舗ID"
    TIMESTAMP created_at "作成日時"
    TIMESTAMP updated_at "更新日時"
  }
  app_designs {
    INTEGER id PK "ID"
    INTEGER shop_id FK "店舗ID"
    VARCHAR json_path "JSONファイル名"
    ENUM layout_type "デザインのテンプレートA~F"
    TIMESTAMP created_at "作成日時"
    TIMESTAMP updated_at "更新日時"
  }
  audience_archives {
    INTEGER id PK "ID"
    INTEGER project_id FK "プロジェクトID"
    INTEGER shop_id FK "ショップID"
    INTEGER trigger_category_id FK "オーディエンスカテゴリID"
    ENUM platform_type "プラットフォーム種別"
    VARCHAR name "オーディエンス名アーカイブ名"
    VARCHAR csv_path "CSVファイルパス"
    TIMESTAMP created_at "作成日時"
    TIMESTAMP updated_at "更新日時"
  }
  audiences {
    INTEGER id PK "ID"
    INTEGER shop_id FK "ショップID"
    VARCHAR name "オーディエンス名"
    TIMESTAMP created_at "作成日時"
    TIMESTAMP updated_at "更新日時"
    INTEGER campaign_id "キャンペーンID"
    INTEGER trigger_id FK "トリガーID"
    INTEGER rank_id FK "ランクID"
    TINYINT is_completed "クーポン利用/未利用・アンケート回答/未回答フラグ"
    VARCHAR value "値"
    INTEGER apply_days "適用日数"
  }
  broadcast_messages {
    INTEGER id PK "ID"
    INTEGER broadcast_id FK "配信ID"
    ENUM type "メッセージタイプ"
    INTEGER message_id "メッセージID"
    INTEGER sort "表示順"
    TIMESTAMP created_at "作成日時"
    TIMESTAMP updated_at "更新日時"
  }
  broadcasts {
    INTEGER id PK "ID"
    INTEGER shop_id FK "ショップID"
    VARCHAR user_ids "配信対象ユーザーID（カンマ区切り）"
    INTEGER audience_id "オーディエンスID（オーディエンス設定用）"
    TEXT current_condition_text "今だけ条件（テキスト）"
    ENUM target "配信対象タイプ（今だけ条件指定 / オーディエンス設定 / 指定会員設定）"
    DATETIME release_datetime "配信日時"
    TINYINT is_draft "下書きフラグ（1:下書き、0:公開）"
    INTEGER headcount "予約中、下書きはNULL"
    INTEGER error_headcount "エラー数"
    DATETIME broadcasted_at "配信日時"
    TIMESTAMP created_at "作成日時"
    TIMESTAMP updated_at "更新日時"
  }
  chat_messages {
    INTEGER id PK "ID"
    INTEGER chatroom_id FK "チャットルームID"
    INTEGER administrator_id FK "管理者ID"
    INTEGER sticker_id FK "チャットスタンプID"
    INTEGER message_id "メッセージID"
    ENUM message_type "メッセージタイプ"
    TEXT content "メッセージ内容"
    TINYINT is_star "スターフラグ"
    VARCHAR file_path "S3パス"
    TINYINT is_read "既読フラグ"
    TINYINT is_done "完了フラグ"
    DATETIME created_at "作成日時"
    DATETIME updated_at "更新日時"
  }
  chatroom_operation_logs {
    INTEGER id PK "ID"
    INTEGER chatroom_id FK "チャットルームID"
    INTEGER administrator_id FK "管理者ID"
    ENUM type "操作タイプ"
    TIMESTAMP created_at "作成日時"
    TIMESTAMP updated_at "更新日時"
  }
  chatroom_scenario_messages {
    INTEGER id PK
    INTEGER chatroom_id FK
    INTEGER scenario_message_id FK
    DATETIME release_datetime
    TIMESTAMP created_at
    TIMESTAMP updated_at
  }
  chatrooms {
    INTEGER id PK "ID"
    INTEGER user_id FK "ユーザーID"
    INTEGER shop_id FK "ショップID"
    INTEGER user_identity_flag_id FK "ユーザー識別フラグID"
    DATETIME user_last_opened_at "ユーザー最終閲覧日時"
    DATETIME admin_last_read_at "管理者最終閲覧日時"
    DATETIME admin_last_done_at "管理者最終完了日時"
    TEXT memo "メモ"
  }
  coupon_settings {
    INTEGER id PK "ID"
    INTEGER shop_id FK "店舗ID"
    INTEGER template_id "テンプレートID"
    TINYINT is_active "有効フラグ"
    TINYINT is_default_image_displayed "デフォルト画像表示フラグ"
    TINYINT is_time_displayed "クーポン表示時間"
    VARCHAR password "パスワード"
    TINYINT is_expiry_notification "クーポン利用期限切れ通知"
  }
  coupons {
    INTEGER id PK "ID"
    INTEGER shop_id FK "ショップID"
    INTEGER rank_id "ランクID"
    INTEGER template_id "テンプレートID"
    VARCHAR display_name "表示名"
    VARCHAR management_name "管理名"
    ENUM type "クーポンタイプ"
    VARCHAR image_path "画像パス"
    VARCHAR description "詳細"
    VARCHAR use_conditions "利用条件"
    INTEGER discount_num "割引数"
    ENUM discount_type "割引タイプ (percent_off: %OFF, fixed_amount: 円引き)"
    ENUM target_type "対象タイプ"
    INTEGER target_new_register_days "新規登録対象日数"
    ENUM target_repeat_category "リピート対象カテゴリ"
    INTEGER target_repeat_value "リピート対象値"
    ENUM target_birth_type "誕生日対象タイプ"
    ENUM target_birth_timing "誕生日対象タイミング"
    TINYINT target_birthday_days "誕生日対象日数"
    DATETIME release_datetime "配信開始日時"
    DATETIME finish_datetime "配信終了日時"
    INTEGER valid_days "有効日数"
    DATETIME expired_at "有効期限"
    INTEGER use_limit "使用制限"
    INTEGER all_distribution_limit "全体配布制限数"
    TIMESTAMP created_at "作成日時"
    TIMESTAMP updated_at "更新日時"
  }
  dealers {
    INTEGER id PK "ID"
    VARCHAR uuid UK "ディーラーUUID"
  }
  fixed_replacement_patterns {
    INTEGER id PK "一意のID"
    INTEGER project_id FK "プロジェクトID"
    VARCHAR status "会員ステータスの置換文字"
    VARCHAR member_id "会員IDの置換文字"
    VARCHAR name "名前の置換文字"
    VARCHAR kana "フリガナの置換文字"
    VARCHAR gender "性別の置換文字"
    VARCHAR birthday "生年月日の置換文字"
    VARCHAR job "職業の置換文字"
    VARCHAR trigger "ご来店のきっかけの置換文字"
    VARCHAR email "メールアドレスの置換文字"
    VARCHAR phone "電話番号の置換文字"
    VARCHAR zipcode "郵便番号の置換文字"
    VARCHAR pref "都道府県の置換文字"
    VARCHAR city "住所（市区町村）の置換文字"
    VARCHAR address "住所（番地、ビル名）の置換文字"
    DATETIME created_at "作成日時"
    DATETIME updated_at "更新日時"
  }
  geofence_logs {
    INTEGER id PK "ID"
    INTEGER user_id FK "ユーザーID"
    INTEGER shop_id FK "店舗ID"
    INTEGER gps_broadcast_id FK "GPS配信ID"
    TINYINT is_inside_geofence "ジオフェンス内判定フラグ"
    TIMESTAMP created_at "作成日時"
  }
  gps_broadcast_messages {
    INTEGER id PK "ID"
    INTEGER gps_broadcast_id FK "GPS配信ID"
    ENUM type "メッセージタイプ"
    INTEGER message_id "メッセージID"
    INTEGER sort "表示順"
    TIMESTAMP created_at "作成日時"
    TIMESTAMP updated_at "更新日時"
  }
  gps_broadcast_weekdays {
    INTEGER id PK "ID"
    INTEGER gps_broadcast_id FK "GPS配信ID"
    TINYINT weekday "曜日（0=日〜6=土）"
  }
  gps_broadcasts {
    INTEGER id PK "ID"
    INTEGER shop_id FK "ショップID"
    INTEGER audience_id FK "オーディエンスID"
    INTEGER gps_setting_id FK "gpsSettingID"
    VARCHAR title "タイトル"
    TINYINT is_scheduled "定期配信フラグ"
    DATETIME schedule_release_datetime "定期配信開始日時"
    DATETIME schedule_finish_datetime "定期配信終了日時"
    TINYINT schedule_day_of_month "日付指定（1〜31）"
    TINYINT is_time_specified "時間指定有無"
    TINYINT start_hour "開始時刻（0〜23）"
    TINYINT end_hour "終了時刻（0〜23）"
    DATETIME finish_datetime "配信終了日時"
    TIMESTAMP created_at "作成日時"
    DATETIME updated_at "更新日時"
  }
  gps_settings {
    INTEGER id PK
    INTEGER shop_id FK "shopID"
    VARCHAR gps_location_name "GPS位置名"
    VARCHAR address "住所"
    DECIMAL latitude "緯度"
    DECIMAL longitude "経度"
    INTEGER radius "半径"
  }
  granted_coupons {
    INTEGER id PK "ID"
    INTEGER user_id FK "ユーザーID"
    INTEGER coupon_id FK "クーポンID"
    TINYINT is_used_up
    DATETIME expired_at
    TIMESTAMP created_at "作成日時"
    TIMESTAMP updated_at "更新日時"
  }
  informations {
    INTEGER id PK "ID"
    INTEGER shop_id FK "店舗ID"
    INTEGER rank_id FK "ランクID"
    ENUM target_type "対象タイプ"
    ENUM category "カテゴリ"
    VARCHAR title "タイトル"
    TEXT content "本文"
    VARCHAR push_notice_title "プッシュ通知タイトル"
    VARCHAR push_notice_content "プッシュ通知本文"
    TINYINT is_draft "下書きフラグ"
    TINYINT is_push_notify "プッシュ通知フラグ"
    DATETIME release_datetime "公開日時"
    VARCHAR guid "GUID"
    VARCHAR image_path "画像パス"
    VARCHAR image_url "画像URL"
    TIMESTAMP created_at
    TIMESTAMP updated_at
    TIMESTAMP deleted_at "削除日時"
  }
  inquiries {
    INTEGER id PK "ID"
    INTEGER shop_id FK "店舗ID"
    INTEGER user_id FK "ユーザーID"
    VARCHAR name "氏名"
    VARCHAR email "メールアドレス"
    TEXT content "お問い合わせ内容"
    TIMESTAMP created_at "作成日時"
    TIMESTAMP updated_at "更新日時"
  }
  makers {
    INTEGER id PK "ID"
    VARCHAR uuid UK "メーカーUUID"
    VARCHAR logo_path "ロゴ画像パス"
    VARCHAR domain UK "メーカードメイン"
  }
  message_card_details {
    INTEGER id PK "ID"
    INTEGER message_card_id FK "配信メッセージカードID"
    ENUM card_type "カードタイプ"
    VARCHAR title "カードタイトル"
    VARCHAR description "説明"
    VARCHAR memo "メモ"
    VARCHAR action_label "アクションラベル"
    ENUM action_type "アクションタイプ"
    VARCHAR action_url "アクションURL"
    ENUM action_display_type "アクション設定タイプ"
    VARCHAR image_path "画像パス"
    INTEGER sort "表示順"
  }
  message_cards {
    INTEGER id PK "ID"
    TIMESTAMP created_at "作成日時"
    TIMESTAMP updated_at "更新日時"
    TIMESTAMP deleted_at "削除日時"
  }
  message_coupons {
    INTEGER id PK "ID"
    INTEGER coupon_id FK "クーポンID"
    TINYINT is_visible_image "画像表示フラグ"
    TIMESTAMP created_at "作成日時"
    TIMESTAMP updated_at "更新日時"
    TIMESTAMP deleted_at "削除日時"
  }
  message_informations {
    INTEGER id PK "ID"
    INTEGER information_id FK "お知らせID"
    TINYINT is_visible_image "画像表示フラグ"
    TIMESTAMP created_at "作成日時"
    TIMESTAMP updated_at "更新日時"
    TIMESTAMP deleted_at "削除日時"
  }
  message_medias {
    INTEGER id PK "ID"
    VARCHAR path "S3パス"
    VARCHAR url "動画URL"
    TIMESTAMP created_at "作成日時"
    TIMESTAMP updated_at "更新日時"
    TIMESTAMP deleted_at "削除日時"
  }
  message_surveys {
    INTEGER id PK "ID"
    INTEGER survey_id FK "アンケートID"
    VARCHAR action_label "アクションラベル"
    TIMESTAMP created_at "作成日時"
    TIMESTAMP updated_at "更新日時"
    TIMESTAMP deleted_at "削除日時"
  }
  message_texts {
    INTEGER id PK "ID"
    TEXT content "内容"
    TIMESTAMP created_at "作成日時"
    TIMESTAMP updated_at "更新日時"
    TIMESTAMP deleted_at "削除日時"
  }
  mypage_settings {
    INTEGER id PK
    INTEGER shop_id FK "店舗ID"
    TINYINT_UNSIGNED is_user_id_displayed "ユーザーID表示フラグ"
    TINYINT is_name_displayed "名前表示フラグ"
    TINYINT is_point_displayed "ポイント表示フラグ"
    TINYINT is_stamp_displayed "スタンプ表示フラグ"
    TINYINT is_coupon_displayed "クーポン表示フラグ"
    TINYINT is_visit_log_displayed "来店履歴表示フラグ"
    TINYINT is_referral_code_displayed "紹介コード表示フラグ"
    TINYINT is_edit_enabled "編集有効フラグ"
    TIMESTAMP created_at
    TIMESTAMP updated_at
  }
  notification_settings {
    INTEGER id PK "ID"
    INTEGER shop_id FK "ショップID"
    TINYINT is_email_transfer_enabled "メール転送有効フラグ"
    VARCHAR transfer_email "転送先メールアドレス"
    TINYINT is_chat_transfer_enabled "チャット転送有効フラグ"
    TINYINT is_user_register_event_notice "ユーザー登録イベント通知フラグ"
    TINYINT is_user_exit_event_notice "ユーザー退会イベント通知フラグ"
    TINYINT is_reservation_complete_event_notice "予約完了イベント通知フラグ"
    TINYINT is_reservation_cancel_event_notice "予約キャンセルイベント通知フラグ"
    TINYINT is_survey_complete_event_notice "アンケート完了イベント通知フラグ"
    TINYINT is_user_visit_event_notice "ユーザー来店イベント通知フラグ"
    TINYINT is_referral_complete_event_notice "紹介完了イベント通知フラグ"
    TINYINT notice_days_before "事前通知日数"
    TINYINT is_coupon_deadline_notice "クーポン期限通知フラグ"
    TINYINT is_point_deadline_notice "ポイント期限通知フラグ"
    TINYINT is_stamp_deadline_notice "スタンプ期限通知フラグ"
    TINYINT is_survey_deadline_notice "アンケート期限通知フラグ"
    TINYINT is_gps_deadline_notice "GPS期限通知フラグ"
    TINYINT is_advertisement_deadline_notice "広告期限通知フラグ"
    TINYINT is_popup_advertisement_deadline_notice "ポップアップ広告期限通知フラグ"
    TINYINT is_information_deadline_notice "お知らせ期限通知フラグ"
  }
  order_informations {
    INTEGER id PK "ID"
    VARCHAR title "タイトル"
    VARCHAR body "本文"
    DATETIME release_datetime "リリース日時"
    DATETIME finish_datetime "公開終了日時"
    ENUM publication_range "公開範囲"
  }
  password_resets {
    INTEGER id PK "ID"
    INTEGER administrator_id FK "管理者ID"
    VARCHAR token "リセットトークン"
    DATETIME expired_at "制限時間"
    TINYINT is_used "使用済みフラグ（0:未使用、1:使用済み）"
    TIMESTAMP created_at "作成日時"
    TIMESTAMP updated_at "更新日時"
  }
  payment_settings {
    INTEGER id PK
    INTEGER shop_id FK "ショップID"
    TINYINT is_paypay_enabled "PayPay決済の有効フラグ"
    TINYINT is_rakuten_pay_enabled "楽天ペイ決済の有効フラグ"
    TINYINT is_d_payment_enabled "d払い決済の有効フラグ"
    TINYINT is_aupay_enabled "auPAY決済の有効フラグ"
    TINYINT is_merpay_enabled "メルペイ決済の有効フラグ"
    TINYINT is_transportation_ic_enabled "交通系IC決済の有効フラグ"
    TINYINT is_rakuten_edy_enabled "楽天Edy決済の有効フラグ"
    TINYINT_UNSIGNED is_id_docomo_enabled "iD(docomo)決済の有効フラグ"
    TINYINT is_quicpay_enabled "QUICPay決済の有効フラグ"
    TINYINT is_visa_enabled "VISA決済の有効フラグ"
    TINYINT is_mastercard_enabled "Mastercard決済の有効フラグ"
    TINYINT is_jcb_enabled "JCB決済の有効フラグ"
    TINYINT is_amex_enabled "American Express決済の有効フラグ"
    TINYINT is_diners_enabled "Diners Club決済の有効フラグ"
    TINYINT is_apple_pay_enabled "Apple Pay決済の有効フラグ"
    TINYINT is_google_pay_enabled "Google Pay決済の有効フラグ"
    TIMESTAMP created_at "作成日時"
    TIMESTAMP updated_at "更新日時"
  }
  point_common_settings {
    INTEGER id PK "ID"
    INTEGER project_id FK "プロジェクトID"
    BIGINT expire_template_id FK "テンプレートID"
    TINYINT is_notify_expired "通知フラグ"
    INTEGER months_since_last_visit "最終来店日からの月数"
    INTEGER months_since_point_grant "ポイント付与日からの月数"
    VARCHAR reward_password "特典パスワード"
    TIMESTAMP created_at "作成日時"
    TIMESTAMP updated_at "更新日時"
  }
  point_logs {
    INTEGER id PK
    INTEGER shop_id FK "店舗ID"
    INTEGER user_id FK "ユーザーID"
    ENUM type "ポイント増減の種別"
    VARCHAR name "履歴タイトル"
    TEXT memo "補足メモ"
    INTEGER point "符号付きポイント値"
    TIMESTAMP created_at "作成日時"
    TIMESTAMP updated_at "更新日時"
  }
  point_rewards {
    INTEGER id PK "ID"
    INTEGER shop_id FK "ショップID"
    INTEGER coupon_id FK "クーポンID"
    ENUM type "特典種別"
    VARCHAR title "タイトル"
    VARCHAR content "内容"
    INTEGER required_point "必要ポイント"
    VARCHAR item "特典アイテム"
    TINYINT is_active "有効フラグ"
  }
  point_settings {
    INTEGER id PK "ID"
    INTEGER shop_id FK "ショップID"
    INTEGER special_point_rule_id FK "特別ポイントルールID"
    INTEGER survey_id FK "アンケートID"
    INTEGER rank_id FK "ランクID"
    ENUM type "タイプ（install: インストール, register: 登録, visit: 来店, sales: 売上, survey: アンケート, rank: ランク, referral: 友達紹介, reserve: 予約, review: 口コミ）"
    INTEGER point "ポイント数"
    INTEGER sales_amount_min "売上倍率最小値"
    INTEGER sales_amount_max "売上倍率最大値"
    INTEGER sales_amount_per "売上倍率金額"
    INTEGER referral_inviter_point "紹介者ポイント"
    INTEGER referral_receiver_point "被紹介者ポイント"
    DECIMAL rank_rate "ランク倍率"
    INTEGER time_period_start_time "時間帯倍率開始時間"
    INTEGER time_period_end_time "時間帯倍率終了時間"
    INTEGER time_period_rate "時間帯倍率"
    TINYINT is_active "有効フラグ"
    TIMESTAMP created_at "作成日時"
    TIMESTAMP updated_at "更新日時"
  }
  point_shop_settings {
    INTEGER id PK "ID"
    INTEGER shop_id FK "店舗ID"
    INTEGER grant_template_id "付与テンプレートID"
    TINYINT is_notify_granted "付与通知フラグ（0:通知しない、1:通知する）"
    TIMESTAMP created_at "作成日時"
    TIMESTAMP updated_at "更新日時"
  }
  point_time_period_weekdays {
    INTEGER id PK "ID"
    INTEGER point_setting_id FK "ポイント設定ID"
    TINYINT weekday "曜日 (0=日,1=月,...6=土)"
  }
  popup_advertisements {
    INTEGER id PK "ID"
    INTEGER shop_id FK "ショップID"
    VARCHAR title "タイトル"
    DATETIME release_datetime "公開日時"
    DATETIME finish_datetime "終了日時"
    INTEGER display_count_limit "表示回数制限"
    VARCHAR image_path "S3パス"
    VARCHAR content "本文"
    TINYINT is_draft "下書きフラグ"
    TINYINT is_priority "優先表示フラグ"
    INTEGER sort "表示順"
    TIMESTAMP created_at "作成日時"
    TIMESTAMP updated_at "更新日時"
  }
  projects {
    INTEGER id PK "ID"
    VARCHAR uuid "案件UUID"
    INTEGER dealer_id "販売店ID"
    INTEGER maker_id
  }
  rank_settings {
    INTEGER id PK "ID"
    INTEGER project_id FK "プロジェクトID"
    TINYINT is_active "有効フラグ"
    TINYINT is_visit_count_enabled "来店回数条件有効フラグ"
    TINYINT is_total_point_enabled "累計ポイント条件有効フラグ"
    TINYINT is_current_point_enabled "現在ポイント条件有効フラグ（保留54）"
    TINYINT is_visit_cycle_enabled "来店サイクル条件有効フラグ"
    TINYINT_UNSIGNED is_paid_average_enabled "平均金額条件有効フラグ"
    TINYINT_UNSIGNED is_paid_total_enabled "累計金額条件有効フラグ"
    INTEGER min_required_count "最小必要数"
    TINYINT grace_period_months "猶予期間（月）"
    TIMESTAMP created_at "作成日時"
    TIMESTAMP updated_at "更新日時"
  }
  ranks {
    INTEGER id PK
    INTEGER project_id FK "プロジェクトID"
    VARCHAR name "ランク名"
    INTEGER visit_count_min "最小訪問回数"
    INTEGER total_point_min "最小累計ポイント"
    INTEGER current_point_min "最小現在ポイント"
    INTEGER visit_cycle_min "最小訪問サイクル"
    INTEGER paid_average_min "最小平均支払金額"
    INTEGER paid_total_min "最小累計支払金額"
    VARCHAR color_code "カラーコード"
    INTEGER rank_position "ランク表示位置"
    TIMESTAMP created_at
    TIMESTAMP updated_at
  }
  referral_reward_settings {
    INTEGER id PK "ID"
    INTEGER shop_id FK "ショップID"
    BIGINT inviter_template_id "被紹介者用テンプレートID"
    BIGINT receiver_template_id FK "紹介者用テンプレートID"
    TINYINT is_active "有効フラグ"
    INTEGER inviter_coupon_id FK "紹介者クーポンID"
    INTEGER receiver_coupon_id FK "被紹介者クーポンID"
    ENUM referrer_reward_condition "紹介者報酬条件（registered: 登録済, reserved: 予約済, visited: 来店済み）"
    ENUM receiver_reward_condition "被紹介者報酬条件（registered: 登録済, reserved: 予約済, visited: 来店済み）"
    INTEGER invite_limit "紹介上限数"
  }
  referral_settings {
    INTEGER id PK "ID"
    INTEGER shop_id FK "店舗ID"
    TINYINT is_line "LINE表示フラグ（0: 非表示, 1: 表示）"
    TINYINT is_x "X表示フラグ（0: 非表示, 1: 表示）"
    TINYINT is_tiktok "TikTok表示フラグ（0: 非表示, 1: 表示）"
    TINYINT is_instagram "Instagram表示フラグ（0: 非表示, 1: 表示）"
    TINYINT is_facebook "Facebook表示フラグ（0: 非表示, 1: 表示）"
    VARCHAR title "タイトル"
    VARCHAR image_path "S3パス"
    VARCHAR announcement_text "お知らせテキスト"
  }
  referral_users {
    INTEGER id PK "ID"
    INTEGER inviter_user_id FK "紹介者ユーザーID"
    INTEGER receiver_user_id FK "紹介された受信者ユーザーID"
    INTEGER inviter_coupon_id FK "紹介者クーポンID"
    INTEGER receiver_coupon_id FK "受信者クーポンID"
    TIMESTAMP achieved_by_receiver_at "受信者達成日時"
    TIMESTAMP created_at "作成日時"
    TIMESTAMP updated_at "更新日時"
  }
  routings {
    INTEGER id PK
    VARCHAR shop_uuid "ショップUUID"
    VARCHAR maker_domain "メーカードメイン"
    VARCHAR project_schema_name "プロジェクトスキーマ名"
    TIMESTAMP created_at
    TIMESTAMP updated_at
  }
  scenario_messages {
    INTEGER id PK "ID"
    INTEGER scenario_id FK "シナリオID"
    TINYINT step_position "ステップ位置"
    INTEGER step_broadcast_interval "ステップ配信間隔"
    ENUM type "メッセージタイプ"
    INTEGER message_id "メッセージID"
    INTEGER sort "表示順"
    TIMESTAMP created_at "作成日時"
    TIMESTAMP updated_at "更新日時"
  }
  scenarios {
    INTEGER id PK
    INTEGER shop_id FK "店舗ID"
    INTEGER coupon_id FK "クーポンID"
    INTEGER survey_id FK "アンケートID"
    VARCHAR user_ids "ユーザーIDリスト（指定会員設定用）"
    INTEGER audience_id "オーディエンスID（オーディエンス設定用）"
    TEXT current_condition_text "今だけ条件（テキスト）"
    ENUM target "配信対象タイプ（今だけ条件指定 / オーディエンス設定 / 指定会員設定）"
    VARCHAR title
    ENUM trigger "トリガータイプ（会員登録、予約完了、来店日、最終ログイン、クーポン、アンケート、友達紹介成立）"
    TINYINT broadcast_hour "配信時刻（時）"
    TINYINT is_active "有効フラグ"
    BOOLEAN is_delivery_restriction
    TIMESTAMP created_at
    TIMESTAMP updated_at
    TIMESTAMP deleted_at
  }
  schema_migrations {
    BIGINT version PK
    TINYINT(1) dirty
  }
  shop_administrators {
    INTEGER id PK "ID"
    INTEGER shop_id FK "店舗ID"
    INTEGER administrator_id FK "管理者ID"
    TIMESTAMP created_at "作成日時"
    TIMESTAMP updated_at "更新日時"
  }
  shop_settings {
    INTEGER id PK "ID"
    INTEGER shop_id FK "店舗ID"
    DECIMAL latitude "緯度"
    DECIMAL longitude "経度"
    INTEGER radius "有効範囲半径"
    VARCHAR gps_location_name "GPS位置名称"
    VARCHAR visit_qr_path "来店QRパス"
    TINYINT is_visit_qr_enabled "来店QR有効フラグ"
    TINYINT is_chat_read_enabled "チャット既読有効フラグ"
    TINYINT is_survey_enabled "アンケート有効フラグ"
    TINYINT is_ever_visit_qr_downloaded "来店QRダウンロード済みフラグ"
    TIMESTAMP created_at "作成日時"
    TIMESTAMP updated_at "更新日時"
    TIMESTAMP deleted_at "削除日時"
  }
  shops {
    INTEGER id PK "ID"
    INTEGER project_id FK "プロジェクトID"
    VARCHAR uuid "店舗UUID"
    INTEGER prefecture_id "都道府県ID"
    VARCHAR name "店舗名"
    VARCHAR main_visual_image_path "店舗メインビジュアル画像パス"
    VARCHAR furigana "フリガナ"
    TINYINT is_wifi_displayed "WiFi表示フラグ"
    VARCHAR wifi_comment "WiFiコメント"
    VARCHAR wifi_ssid "WiFi SSID"
    VARCHAR wifi_password "WiFiパスワード"
    VARCHAR email "メールアドレス"
    VARCHAR postal_code "郵便番号"
    VARCHAR address_city "住所（市区町村）"
    VARCHAR address_detail "住所（番地、ビル名）"
    VARCHAR tel "電話番号"
    VARCHAR shop_url "店舗URL"
    VARCHAR business_hours_text "営業時間テキスト"
    VARCHAR closed_day_text "定休日テキスト"
    TINYINT closing_time "閉店時間"
    VARCHAR access_info "アクセス情報"
    VARCHAR description "店舗説明"
    VARCHAR primary_industry
    VARCHAR secondary_industry
    TIMESTAMP created_at "作成日時"
    TIMESTAMP updated_at "更新日時"
    TIMESTAMP deleted_at "削除日時"
  }
  special_point_rules {
    INTEGER id PK "ID"
    INTEGER shop_id FK "店舗ID"
    INTEGER grant_template_id "付与テンプレートID"
    VARCHAR name "ルール名"
    DATETIME release_datetime "適用期間開始日時"
    DATETIME finish_datetime "適用期間終了日時"
    TINYINT is_active "有効フラグ"
    TINYINT is_notify_granted "付与通知フラグ"
    TIMESTAMP created_at "作成日時"
    TIMESTAMP updated_at "更新日時"
  }
  special_stamp_rules {
    INTEGER id PK "ID"
    INTEGER shop_id FK "店舗ID"
    INTEGER grant_template_id "スタンプ付与テンプレートID"
    VARCHAR name "ルール名"
    DATETIME release_datetime "適用期間開始日時"
    DATETIME finish_datetime "適用期間終了日時"
    TINYINT is_notify_granted "付与通知フラグ"
    TIMESTAMP created_at "作成日時"
    TIMESTAMP updated_at "更新日時"
  }
  spent_coupon_logs {
    INTEGER id PK "ID"
    INTEGER granted_coupon_id FK "付与クーポンID"
    TIMESTAMP created_at "作成日時"
    TIMESTAMP updated_at "更新日時"
  }
  stamp_common_settings {
    INTEGER id PK "ID"
    INTEGER project_id FK "プロジェクトID"
    INTEGER expire_template_id FK "テンプレートID"
    TINYINT is_notify_expired "通知フラグ"
    INTEGER months_since_last_visit "最終来店日からの月数"
    INTEGER months_since_stamp_grant "スタンプ付与日からの月数"
    TINYINT is_qr_grant "スタンプをQRで付与"
    TINYINT is_nfc_grant "スタンプをNFCで付与"
    INTEGER stamp_card_max_count "スタンプカードの最大個数"
    ENUM display_frame_type "スタンプカードの枠の形（circle: 丸, rounded: 角丸）"
    TIMESTAMP created_at "作成日時"
    TIMESTAMP updated_at "更新日時"
  }
  stamp_logs {
    INTEGER id PK "ID"
    INTEGER shop_id FK "店舗ID"
    INTEGER user_id FK "ユーザーID"
    ENUM type "タイプ"
    VARCHAR name "名前"
    INTEGER stamp "スタンプ"
    VARCHAR memo "メモ"
    TIMESTAMP created_at "作成日時"
    TIMESTAMP updated_at "更新日時"
  }
  stamp_rewards {
    INTEGER id PK "ID"
    INTEGER shop_id FK "ショップID"
    INTEGER coupon_id FK "クーポンID"
    ENUM type "特典種別"
    VARCHAR title "タイトル"
    INTEGER required_stamp "必要スタンプ"
    VARCHAR item "特典アイテム"
    INTEGER point "ポイント"
    TINYINT is_active "有効フラグ"
    DATETIME release_datetime "適用期間開始日時"
    DATETIME finish_datetime "適用期間終了日時"
  }
  stamp_settings {
    INTEGER id PK "ID"
    INTEGER shop_id FK "ショップID"
    INTEGER special_stamp_rule_id FK "特別スタンプルールID"
    INTEGER survey_id FK "アンケートID"
    INTEGER rank_id FK "ランクID"
    ENUM type "タイプ（install: インストール, register: 登録, visit: 来店, sales: 売上, survey: アンケート, rank: ランク, referral: 友達紹介, reserve: 予約, review: 口コミ）"
    INTEGER stamp "スタンプ数"
    INTEGER sales_amount_min "売上倍率最小値"
    INTEGER sales_amount_max "売上倍率最大値"
    INTEGER sales_amount_per "売上倍率金額"
    INTEGER referral_inviter_stamp "紹介者スタンプ"
    INTEGER referral_receiver_stamp "被紹介者スタンプ"
    INTEGER rank_bonus_stamps "ランク倍率"
    INTEGER time_period_start_time "時間帯倍率開始時間"
    INTEGER time_period_end_time "時間帯倍率終了時間"
    INTEGER time_period_rate "時間帯倍率"
    TIMESTAMP created_at "作成日時"
    TIMESTAMP updated_at "更新日時"
  }
  stamp_shop_settings {
    INTEGER id PK "ID"
    INTEGER shop_id FK "ショップID"
    INTEGER grant_template_id FK "付与テンプレートID"
    TINYINT is_notify_granted "付与通知フラグ"
  }
  stamp_time_period_weekdays {
    INTEGER id PK "ID"
    INTEGER stamp_setting_id FK "スタンプ設定ID"
    TINYINT weekday "曜日 (0=日,1=月,...6=土)"
  }
  stickers {
    INTEGER id PK "ID"
    INTEGER shop_id FK "販売店ID"
    VARCHAR path "S3パス"
    TIMESTAMP deleted_at "削除日時"
  }
  survey_analyses {
    INTEGER id PK
    INTEGER survey_id
    DATE date
    INTEGER view_count
    INTEGER answer_count
  }
  survey_answer_choices {
    INTEGER id PK "ID"
    INTEGER survey_answer_id FK "アンケート回答ID"
    INTEGER survey_question_option_id FK "アンケート質問オプションID"
  }
  survey_answer_texts {
    INTEGER id PK "ID"
    INTEGER survey_answer_id FK "アンケート回答ID"
    INTEGER survey_question_id FK "アンケート質問ID"
    VARCHAR text "回答テキスト"
  }
  survey_answers {
    INTEGER id PK "ID"
    INTEGER user_id FK "ユーザーID"
    INTEGER survey_id FK "アンケートID"
    INTEGER review_rate "評価レート"
    TINYINT is_external_review_access "外部レビューアクセスフラグ"
    DATETIME created_at "作成日時"
    DATETIME updated_at "更新日時"
  }
  survey_question_options {
    INTEGER id PK "ID"
    INTEGER survey_question_id "アンケート質問ID"
    VARCHAR name "名前"
  }
  survey_questions {
    INTEGER id PK "ID"
    INTEGER survey_id FK "アンケートID"
    VARCHAR title "タイトル"
    VARCHAR description "説明"
    ENUM type "質問タイプ（short_text: 短文テキスト, long_text: 長文テキスト, radio: ラジオボタン, checkbox: チェックボックス, dropdown: ドロップダウン）"
    TINYINT is_required "必須フラグ（1: 必須, 0: 任意）"
    DATETIME created_at "作成日時"
    DATETIME updated_at "更新日時"
  }
  surveys {
    INTEGER id PK "ID"
    INTEGER shop_id FK "ショップID"
    INTEGER coupon_id FK "クーポンID"
    INTEGER template_id FK "サンクスメッセージ用テンプレートID"
    VARCHAR name "アンケート名"
    INTEGER answer_limit "回答上限数"
    TINYINT is_instant "即時配信フラグ"
    INTEGER distribution_later_days "来店後配信までの日数"
    DATETIME distribution_datetime "配信日時"
    TINYINT is_notify_admin "管理者通知フラグ"
    TINYINT is_external_review_enabled "外部レビュー有効フラグ"
    VARCHAR external_review_url "外部レビューURL"
    TINYINT is_review_criteria_question_displayed "評価質問表示フラグ"
    INTEGER star_threshold "星評価のしきい値"
    TINYINT is_external_review_question_displayed "外部口コミ質問表示フラグ"
    VARCHAR thanks_modal_text "サンクスモーダルテキスト"
    DATETIME created_at "作成日時"
    DATETIME updated_at "更新日時"
    TIMESTAMP deleted_at "削除日時"
  }
  template_messages {
    INTEGER id PK "ID"
    INTEGER template_id FK "テンプレートID"
    ENUM type "メッセージタイプ"
    INTEGER message_id "メッセージID"
    INTEGER sort "表示順"
    TIMESTAMP created_at "作成日時"
    TIMESTAMP updated_at "更新日時"
  }
  template_settings {
    INTEGER id PK "ID"
    INTEGER template_id FK "メッセージテンプレートID"
    JSON settings "配信設定詳細 (JSON形式)"
    TIMESTAMP created_at "作成日時"
    TIMESTAMP updated_at "更新日時"
    VARCHAR recurring_type "定期配信タイプ(monthly/weekly)"
    TINYINT recurring_day_of_month "月次配信の日"
    VARCHAR recurring_day_of_week
    VARCHAR event_type "イベントタイプ(birthday等)"
    VARCHAR timing_rule_type "タイミングルールタイプ"
    INTEGER timing_rule_days "オフセット日数"
    INTEGER timing_rule_day "月内の特定日"
  }
  templates {
    INTEGER id PK "ID"
    INTEGER project_id FK "プロジェクトID"
    INTEGER shop_id FK "店舗ID"
    ENUM category "メッセージカテゴリ (クーポン, アンケート, 予約, ポイント, 友達紹介, 定期配信, イベント)"
    VARCHAR title "タイトル"
    TIMESTAMP created_at "作成日時"
    TIMESTAMP updated_at "更新日時"
    TIMESTAMP deleted_at "削除日時"
  }
  trigger_categories {
    INTEGER id PK "ID"
    VARCHAR name "トリガーカテゴリ名"
  }
  triggers {
    INTEGER id PK "ID"
    INTEGER trigger_category_id FK "オーディエンスカテゴリID"
    VARCHAR name "トリガー名"
    INTEGER fixed_text_category "固定テキストカテゴリー"
  }
  user_custom_field_choices {
    INTEGER id PK "ID"
    INTEGER user_custom_field_id FK "カスタム質問ID"
    VARCHAR value "選択肢の値"
    TIMESTAMP created_at "作成日時"
    TIMESTAMP updated_at "更新日時"
  }
  user_custom_fields {
    INTEGER id PK
    INTEGER project_id FK
    VARCHAR title
    TINYINT is_required
    ENUM answer_format
    ENUM category
    INTEGER string_max_num
    INTEGER string_min_num
    TINYINT is_registration_form_display
    TINYINT is_edit_page_display
    VARCHAR original_string
    VARCHAR default_converted_string
  }
  user_custom_values {
    INTEGER id PK "ID"
    INTEGER user_id FK "ユーザーID"
    INTEGER user_custom_field_id FK "カスタム質問ID"
    TEXT answer "回答内容"
    INTEGER user_custom_field_choice_id FK "カスタム質問選択肢ID"
    TIMESTAMP created_at "作成日時"
    TIMESTAMP updated_at "更新日時"
  }
  user_devices {
    INTEGER id PK
    INTEGER user_id FK "ユーザーID"
    VARCHAR udid "UDID"
    VARCHAR push_device_id "プッシュデバイスID"
    ENUM os_type "OSタイプ"
    VARCHAR os_version "OSバージョン"
    VARCHAR user_agent "ユーザーエージェント"
    TIMESTAMP created_at
    TIMESTAMP updated_at
  }
  user_identity_flags {
    INTEGER id PK "ID"
    INTEGER shop_id FK "店舗ID"
    VARCHAR name "名前"
    INTEGER sort "表示順"
    TIMESTAMP created_at "作成日時"
    TIMESTAMP updated_at "更新日時"
  }
  user_points {
    INTEGER id PK "ID"
    INTEGER user_id FK "ユーザーID"
    INTEGER current_balance "現在の残高"
    DATE first_granted_date "初回付与日"
    TIMESTAMP created_at "作成日時"
    TIMESTAMP updated_at "更新日時"
  }
  user_profiles {
    INTEGER id PK "ID"
    INTEGER user_id FK "ユーザーID"
    INTEGER prefecture_id "都道府県ID"
    VARCHAR name "名前"
    VARCHAR furigana "フリガナ"
    VARCHAR postal_code "郵便番号"
    VARCHAR address_city "住所（市区町村）"
    VARCHAR address_detail "住所（番地、ビル名）"
    VARCHAR tel "電話番号"
    ENUM gender "性別"
    DATETIME birthdate "生年月日"
    ENUM job "職業"
    ENUM visit_trigger "来店きっかけ"
    VARCHAR tag_string "管理者タグ"
    TEXT memo "管理者メモ"
    VARCHAR icon_path "アイコンパス"
    TIMESTAMP created_at "作成日時"
    TIMESTAMP updated_at "更新日時"
  }
  user_register_settings {
    INTEGER id PK "ID"
    INTEGER project_id FK "プロジェクトID"
    TINYINT is_promotive_enabled "会員登録の促しフラグ"
    TINYINT is_skip_enabled "会員登録スキップフラグ"
    TIMESTAMP created_at "作成日時"
    TIMESTAMP updated_at "更新日時"
  }
  user_settings {
    INTEGER id PK "ID"
    VARCHAR user_uuid FK "ユーザーID"
    TINYINT is_reminder_enabled "リマインダー設定状況"
    TINYINT is_email_notified "配信チャット通知フラグ"
    TINYINT is_push_notified "プッシュ通知フラグ"
    TIMESTAMP created_at "作成日時"
    TIMESTAMP updated_at "更新日時"
  }
  user_stamp_rewards {
    INTEGER id PK "ID"
    INTEGER user_id FK "ユーザーID"
    INTEGER stamp_reward_id FK "スタンプ特典ID"
    DATETIME used_at "使用日時"
    TIMESTAMP created_at "作成日時"
    TIMESTAMP updated_at "更新日時"
  }
  users {
    INTEGER id PK "ID"
    VARCHAR uuid "ユーザーUUID"
    VARCHAR uid UK "Firebase UID"
    INTEGER project_id FK "プロジェクトID"
    INTEGER shop_id FK "店舗ID"
    INTEGER rank_id FK "ランクID"
    VARCHAR email "メールアドレス"
    VARCHAR password "パスワード"
    ENUM entry_type "会員登録方法"
    TINYINT is_banned "垢BANフラグ"
    DATETIME leave_date "退会日"
    TIMESTAMP registered_at "会員登録日時"
    TIMESTAMP last_logged_in_at "最終ログイン日時"
    VARCHAR referral_code "紹介コード"
    TIMESTAMP rank_not_achieved_at "ランク未達成日時"
    TIMESTAMP referral_deactivated_at "紹介コード無効化日時"
    TIMESTAMP created_at "作成日時"
    TIMESTAMP updated_at "更新日時"
  }
  visit_authentication_settings {
    INTEGER id PK "ID"
    INTEGER shop_id FK "店舗ID"
    TINYINT is_wifi_enabled "WiFi認証有効フラグ"
    VARCHAR wifi_ssid "WiFi SSID"
    TINYINT is_nfc_enabled "NFC認証有効フラグ"
    TINYINT is_gps_enabled "GPS認証有効フラグ"
    TINYINT is_qr_enabled "ポイントカード認証有効フラグ"
    TINYINT is_reservation_enabled "予約認証有効フラグ"
    TIMESTAMP created_at "作成日時"
    TIMESTAMP updated_at "更新日時"
  }
  visit_logs {
    INTEGER id PK "ID"
    INTEGER user_id FK "ユーザーID"
    INTEGER shop_id FK "店舗ID"
    ENUM type "来店タイプ"
    INTEGER sales_amount
    TIMESTAMP created_at "作成日時"
    TIMESTAMP updated_at "更新日時"
  }
  shops ||--o{ advertisements : "fk_shops_id_advertisements"
  shops ||--o{ analysis_reports : "fk_shops_id_analysis_reports"
  shops ||--o{ app_designs : "fk_shops_id_app_designs"
  projects ||--o{ audience_archives : "fk_projects_id_audience_archives"
  shops ||--o{ audience_archives : "fk_shops_id_audience_archives"
  trigger_categories ||--o{ audience_archives : "fk_trigger_categories_id_audience_archives"
  shops ||--o{ audiences : "fk_shops_id_audiences"
  broadcasts ||--o{ broadcast_messages : "fk_broadcasts_id_broadcast_messages"
  shops ||--o{ broadcasts : "fk_shops_id_broadcasts"
  chatrooms ||--o{ chat_messages : "fk_chatrooms_id_chat_messages"
  administrators ||--o{ chat_messages : "fk_administrators_id_chat_messages"
  stickers ||--o{ chat_messages : "fk_stickers_id_chat_messages"
  chatrooms ||--o{ chatroom_operation_logs : "fk_chatrooms_id_chatroom_operation_logs"
  administrators ||--o{ chatroom_operation_logs : "fk_administrators_id_chatroom_operation_logs"
  chatrooms ||--o{ chatroom_scenario_messages : "fk_chatrooms_id_chatroom_scenario_messages"
  scenario_messages ||--o{ chatroom_scenario_messages : "fk_scenario_messages_id_chatroom_scenario_messages"
  shops ||--o{ chatrooms : "fk_shops_id_chatrooms"
  user_identity_flags ||--o{ chatrooms : "fk_user_identity_flags_id_chatrooms"
  shops ||--o{ coupon_settings : "fk_shops_id_coupon_settings"
  shops ||--o{ coupons : "fk_shops_id_coupons"
  projects ||--o{ fixed_replacement_patterns : "fk_projects_id_fixed_replacement_patterns"
  gps_broadcasts ||--o{ gps_broadcast_messages : "fk_gps_broadcasts_id_gps_broadcast_messages"
  gps_broadcasts ||--o{ gps_broadcast_weekdays : "fk_gps_broadcasts_id_gps_broadcast_weekdays"
  shops ||--o{ gps_broadcasts : "fk_shops_id_gps_broadcasts"
  audiences ||--o{ gps_broadcasts : "fk_audiences_id_gps_broadcasts"
  coupons ||--o{ granted_coupons : "fk_coupons_id_granted_coupons"
  users ||--o{ granted_coupons : "fk_users_id_granted_coupons"
  shops ||--o{ informations : "fk_shops_id_informations"
  ranks ||--o{ informations : "fk_ranks_id_informations"
  shops ||--o{ inquiries : "fk_shops_id_inquiries"
  message_cards ||--o{ message_card_details : "fk_message_cards_id_message_card_details"
  coupons ||--o{ message_coupons : "fk_coupons_id_message_coupons"
  informations ||--o{ message_informations : "fk_informations_id_message_informations"
  surveys ||--o{ message_surveys : "fk_surveys_id_message_surveys"
  shops ||--o{ mypage_settings : "fk_shops_id_mypage_settings"
  shops ||--o{ notification_settings : "fk_shops_id_notification_settings"
  administrators ||--o{ password_resets : "fk_administrators_id_password_resets"
  shops ||--o{ payment_settings : "fk_shops_id_payment_settings"
  projects ||--o{ point_common_settings : "fk_projects_id_point_common_settings"
  templates ||--o{ point_common_settings : "fk_templates_id_point_common_settings"
  shops ||--o{ point_rewards : "fk_shops_id_point_rewards"
  coupons ||--o{ point_rewards : "fk_coupons_id_point_rewards"
  shops ||--o{ point_settings : "fk_shops_id_point_settings"
  special_point_rules ||--o{ point_settings : "fk_special_point_rules_id_point_settings"
  surveys ||--o{ point_settings : "fk_surveys_id_point_settings"
  ranks ||--o{ point_settings : "fk_ranks_id_point_settings"
  shops ||--o{ point_shop_settings : "fk_shops_id_point_shop_settings"
  point_settings ||--o{ point_time_period_weekdays : "fk_point_settings_id_point_time_period_weekdays"
  shops ||--o{ popup_advertisements : "fk_shops_id_popup_advertisements"
  projects ||--o{ rank_settings : "fk_projects_id_rank_settings"
  projects ||--o{ ranks : "fk_projects_id_ranks"
  shops ||--o{ referral_reward_settings : "fk_shops_id_referral_reward_settings"
  coupons ||--o{ referral_reward_settings : "fk_coupons_id_referral_reward_settings"
  coupons ||--o{ referral_reward_settings : "fk_coupons_id_referral_reward_settings"
  templates ||--o{ referral_reward_settings : "fk_templates_id_referral_reward_settings"
  shops ||--o{ referral_settings : "fk_shops_id_referral_settings"
  users ||--o{ referral_users : "fk_users_id_referral_users"
  users ||--o{ referral_users : "fk_users_id_referral_users"
  coupons ||--o{ referral_users : "fk_coupons_id_referral_users"
  coupons ||--o{ referral_users : "fk_coupons_id_referral_users"
  scenarios ||--o{ scenario_messages : "fk_scenarios_id_scenario_messages"
  coupons ||--o{ scenarios : "fk_coupons_id_scenarios"
  shops ||--o{ scenarios : "fk_shops_id_scenarios"
  surveys ||--o{ scenarios : "fk_surveys_id_scenarios"
  shops ||--o{ shop_administrators : "fk_shops_id_shop_administrators"
  administrators ||--o{ shop_administrators : "fk_administrators_id_shop_administrators"
  shops ||--o{ shop_settings : "fk_shops_id_shop_settings"
  projects ||--o{ shops : "fk_projects_id_shops"
  shops ||--o{ special_point_rules : "fk_shops_id_special_point_rules"
  shops ||--o{ special_stamp_rules : "fk_shops_id_special_stamp_rules"
  granted_coupons ||--o{ spent_coupon_logs : "fk_granted_coupons_id_spent_coupon_logs"
  projects ||--o{ stamp_common_settings : "fk_projects_id_stamp_common_settings"
  templates ||--o{ stamp_common_settings : "fk_templates_id_stamp_common_settings"
  shops ||--o{ stamp_logs : "fk_shops_id_stamp_logs"
  users ||--o{ stamp_logs : "fk_users_id_stamp_logs"
  shops ||--o{ stamp_rewards : "fk_shops_id_stamp_rewards"
  coupons ||--o{ stamp_rewards : "fk_coupons_id_stamp_rewards"
  shops ||--o{ stamp_settings : "fk_shops_id_stamp_settings"
  special_stamp_rules ||--o{ stamp_settings : "fk_special_stamp_rules_id_stamp_settings"
  surveys ||--o{ stamp_settings : "fk_surveys_id_stamp_settings"
  ranks ||--o{ stamp_settings : "fk_ranks_id_stamp_settings"
  shops ||--o{ stamp_shop_settings : "fk_shops_id_stamp_shop_settings"
  templates ||--o{ stamp_shop_settings : "fk_templates_id_stamp_shop_settings"
  stamp_settings ||--o{ stamp_time_period_weekdays : "fk_stamp_settings_id_stamp_time_period_weekdays"
  shops ||--o{ stickers : "fk_shops_id_stickers"
  survey_answers ||--o{ survey_answer_choices : "fk_survey_answers_id_survey_answer_choices"
  survey_question_options ||--o{ survey_answer_choices : "fk_survey_question_options_id_survey_answer_choices"
  survey_answers ||--o{ survey_answer_texts : "fk_survey_answers_id_survey_answer_texts"
  survey_questions ||--o{ survey_answer_texts : "fk_survey_questions_id_survey_answer_texts"
  users ||--o{ survey_answers : "fk_users_id_survey_answers"
  surveys ||--o{ survey_answers : "fk_surveys_id_survey_answers"
  surveys ||--o{ survey_questions : "fk_surveys_id_survey_questions"
  shops ||--o{ surveys : "fk_shops_id_surveys"
  coupons ||--o{ surveys : "fk_coupons_id_surveys"
  templates ||--o{ surveys : "fk_templates_id_surveys"
  templates ||--o{ template_messages : "fk_templates_id_template_messages"
  templates ||--o{ template_settings : "fk_templates_id_template_settings"
  projects ||--o{ templates : "fk_projects_id_templates"
  shops ||--o{ templates : "fk_shops_id_templates"
  trigger_categories ||--o{ triggers : "fk_trigger_categories_id_triggers"
  user_custom_fields ||--o{ user_custom_field_choices : "fk_user_custom_fields_id_user_custom_field_choices"
  projects ||--o{ user_custom_fields : "fk_projects_id_user_custom_fields"
  user_custom_field_choices ||--o{ user_custom_values : "fk_user_custom_field_choices_id_user_custom_values"
  user_custom_fields ||--o{ user_custom_values : "fk_user_custom_fields_id_user_custom_values"
  users ||--o{ user_custom_values : "fk_users_id_user_custom_values"
  shops ||--o{ user_identity_flags : "fk_shops_id_user_identity_flags"
  users ||--o{ user_points : "fk_users_id_user_points"
  users ||--o{ user_profiles : "fk_users_id_user_profiles"
  projects ||--o{ user_register_settings : "fk_projects_id_user_register_settings"
  users ||--o{ user_settings : "fk_users_id_user_settings"
  users ||--o{ user_stamp_rewards : "fk_users_id_user_stamp_rewards"
  stamp_rewards ||--o{ user_stamp_rewards : "fk_stamp_rewards_id_user_stamp_rewards"
  projects ||--o{ users : "fk_projects_id_users"
  shops ||--o{ users : "fk_shops_id_users"
  ranks ||--o{ users : "fk_ranks_id_users"
  shops ||--o{ visit_authentication_settings : "fk_shops_id_visit_authentication_settings"
  shops ||--o{ visit_logs : "fk_shops_id_visit_logs"
  users ||--o{ visit_logs : "fk_users_id_visit_logs"
  chatrooms }o--|| users : "fk_chatrooms_user_id_users"
  user_devices }o--|| users : "fk_user_devices_user_id_users"
  inquiries }o--|| users : "fk_inquiries_user_id_users"
  triggers ||--o{ audiences : "fk_triggers_id_audiences"
  ranks ||--o{ audiences : "fk_ranks_id_audiences"
  gps_broadcasts }o--|| gps_settings : "fk_gps_broadcasts_gps_setting_id_gps_settings"
  gps_settings }o--|| shops : "fk_gps_settings_shop_id_shops"
  shops ||--o{ point_logs : "fk_shops_id_point_logs"
  users ||--o{ point_logs : "fk_users_id_point_logs"
  users ||--o{ geofence_logs : "fk_users_id_geofence_logs"
  shops ||--o{ geofence_logs : "fk_shops_id_geofence_logs"
  gps_broadcasts ||--o{ geofence_logs : "fk_gps_broadcasts_id_geofence_logs"
