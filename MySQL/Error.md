# MySQL 에러 정리

# 1. mysql connection 에러

node에서 mysql을 연동하려고 하는데 이런 에러가 발생했다.

    Error: ER_NOT_SUPPORTED_AUTH_MODE: Client does not support authentication protocol requested by server; consider upgrading MySQL client

구글링을 해보니 MySQL version8을 설치할 때 비밀번호의 수준을  MEDIUM 이상을 선택할 시 저런 에러가 나는 것 같다. 아니면 수준에 맞지 않는 비밀번호를 설정해서 그런것 같기도 하다.

내가 설정한 비밀번호 정책의 수준은 MEDIUM이었다.

    mysql> SHOW VARIABLES LIKE 'validate_password%';
    +--------------------------------------+--------+
    | Variable_name                        | Value  |
    +--------------------------------------+--------+
    | validate_password.check_user_name    | ON     |
    | validate_password.dictionary_file    |        |
    | validate_password.length             | 8      |
    | validate_password.mixed_case_count   | 1      |
    | validate_password.number_count       | 1      |
    | validate_password.policy             | MEDIUM |
    | validate_password.special_char_count | 1      |
    +--------------------------------------+--------+
    7 rows in set (0.01 sec)

## 해결방법

비밀번호 강제 수준을 LOW로 변경.

    SET GLOBAL validate_password.policy=LOW;

연동에 성공했다.
