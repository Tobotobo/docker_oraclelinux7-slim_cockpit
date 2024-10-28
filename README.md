# docker_oraclelinux7-slim_cockpit

## 概要
* oraclelinux:7-slim で cockpit を動かす

## 結果
とりあえずログインはできるようになった  
* [OK]システム
* [NG]ログ
* [NG]ネットワーキング
* [OK]アカウント
* [NG]サービス
* [NG]Diagnostic Reports
* [NG]SELinux
* [???]カーネルダンプ
* [OK]端末

だいたい以下のエラー  
No journal files were found.

## 詳細

docker pull oraclelinux:7-slim

ja.UTF-8 ja_JP.UTF-8

docker compose exec oracle bash
/usr/libexec/cockpit-ws --no-tls -p 9090

localedef -f UTF-8 -i ja_JP ja.UTF-8

```
bash-4.2# /usr/libexec/cockpit-ws --no-tls -p 9090

(cockpit-bridge:19): cockpit-bridge-WARNING **: 06:58:56.133: couldn't start ssh-agent: Child process exited with code 1: 
invalid or unusable locale: ja.UTF-8
Error getting authority: Error initializing authority: Could not connect: No such file or directory
cockpit-protocol-Message: 06:58:56.350: 1:1!6: Could not connect: No such file or directory
cockpit-protocol-Message: 06:58:56.352: 1:5: Could not connect: No such file or directory
cockpit-protocol-Message: 06:58:56.352: 1:1!7: Could not connect: No such file or directory
cockpit-protocol-Message: 06:58:56.352: 1:1!14: (null)
cockpit-protocol-Message: 06:58:56.352: 1:1!21: (null)
cockpit-protocol-Message: 06:58:56.353: 1:1!10: (null)
cockpit-protocol-Message: 06:58:56.415: 1:1!22: Could not connect: No such file or directory
cockpit-protocol-Message: 06:58:56.430: 1:1!24: Could not connect: No such file or directory
cockpit-protocol-Message: 06:58:56.430: 1:1!25: (null)
exec gdb failed: No such file or directory
Error: signal Segmentation fault:
cockpit-bridge(+0x439c9)[0x5ecd69e439c9]
/lib64/libc.so.6(+0x36400)[0x7d34a01ad400]
/lib64/libglib-2.0.so.0(g_slice_alloc+0xa7)[0x7d34a154edd7]
/lib64/libglib-2.0.so.0(g_slist_prepend+0x16)[0x7d34a154fbc6]
/lib64/libgobject-2.0.so.0(+0x1465b)[0x7d34a181065b]
/lib64/libgobject-2.0.so.0(+0x1568c)[0x7d34a181168c]
/lib64/libgobject-2.0.so.0(g_object_new_valist+0x371)[0x7d34a18131b1]
/lib64/libgobject-2.0.so.0(g_object_new+0x99)[0x7d34a18134f9]
cockpit-bridge(+0x2cfc2)[0x5ecd69e2cfc2]
cockpit-bridge(+0x2d39a)[0x5ecd69e2d39a]
cockpit-bridge(+0x2df49)[0x5ecd69e2df49]
/lib64/libffi.so.6(ffi_call_unix64+0x4c)[0x7d349ff74e2c]
/lib64/libffi.so.6(ffi_call+0x1f5)[0x7d349ff74755]
/lib64/libgobject-2.0.so.0(g_cclosure_marshal_generic+0x1f8)[0x7d34a180c258]
/lib64/libgobject-2.0.so.0(g_closure_invoke+0x138)[0x7d34a180ba18]
/lib64/libgobject-2.0.so.0(+0x220fd)[0x7d34a181e0fd]
```

```
bash-4.2# localedef -f UTF-8 -i ja_JP ja.UTF-8
bash-4.2# /usr/libexec/cockpit-ws --no-tls -p 9090

(cockpit-bridge:55): cockpit-bridge-WARNING **: 07:05:41.204: couldn't start ssh-agent: Child process exited with code 1: 
Error getting authority: Error initializing authority: Could not connect: No such file or directory
cockpit-protocol-Message: 07:05:41.393: 1:1!6: Could not connect: No such file or directory
cockpit-protocol-Message: 07:05:41.401: 1:5: Could not connect: No such file or directory
cockpit-protocol-Message: 07:05:41.402: 1:1!7: Could not connect: No such file or directory
cockpit-protocol-Message: 07:05:41.402: 1:1!14: (null)
cockpit-protocol-Message: 07:05:41.402: 1:1!21: (null)
cockpit-protocol-Message: 07:05:41.402: 1:1!10: (null)
cockpit-protocol-Message: 07:05:41.435: 1:1!22: Could not connect: No such file or directory
cockpit-protocol-Message: 07:05:41.449: 1:1!24: Could not connect: No such file or directory
cockpit-protocol-Message: 07:05:41.450: 1:1!25: Could not connect: No such file or directory
exec gdb failed: そのようなファイルやディレクトリはありません
Error: signal Segmentation fault:
cockpit-bridge(+0x439c9)[0x5d4e832439c9]
/lib64/libc.so.6(+0x36400)[0x79a1a9a50400]
/lib64/libglib-2.0.so.0(g_slice_alloc+0xa7)[0x79a1aadf1dd7]
/lib64/libglib-2.0.so.0(g_slist_prepend+0x16)[0x79a1aadf2bc6]
/lib64/libglib-2.0.so.0(g_strsplit+0xd9)[0x79a1aadf4e69]
cockpit-bridge(+0x1aadb)[0x5d4e8321aadb]
cockpit-bridge(+0x19f3d)[0x5d4e83219f3d]
cockpit-bridge(+0x1afae)[0x5d4e8321afae]
cockpit-bridge(+0x1a96e)[0x5d4e8321a96e]
cockpit-bridge(+0x3b772)[0x5d4e8323b772]
/lib64/libglib-2.0.so.0(+0x48d47)[0x79a1aadd1d47]
/lib64/libglib-2.0.so.0(g_main_context_dispatch+0x159)[0x79a1aadd5119]
/lib64/libglib-2.0.so.0(+0x4c478)[0x79a1aadd5478]
/lib64/libglib-2.0.so.0(g_main_context_iteration+0x2c)[0x79a1aadd552c]
cockpit-bridge(+0x135a4)[0x5d4e832135a4]
/lib64/libc.so.6(__libc_start_main+0xf5)[0x79a1a9a3c555]
```

```
yum install -y openssh-clients
bash-4.2# /usr/libexec/cockpit-ws --no-tls -p 9090
Error getting authority: Error initializing authority: Could not connect: No such file or directory
cockpit-protocol-Message: 07:10:52.411: 1:1!6: Could not connect: No such file or directory
cockpit-protocol-Message: 07:10:52.418: 1:5: Could not connect: No such file or directory
cockpit-protocol-Message: 07:10:52.418: 1:1!7: Could not connect: No such file or directory
cockpit-protocol-Message: 07:10:52.418: 1:1!14: (null)
cockpit-protocol-Message: 07:10:52.418: 1:1!21: (null)
cockpit-protocol-Message: 07:10:52.418: 1:1!10: (null)
cockpit-protocol-Message: 07:10:52.424: 1:1!22: Could not connect: No such file or directory
cockpit-protocol-Message: 07:10:52.454: 1:1!24: Could not connect: No such file or directory
cockpit-protocol-Message: 07:10:52.454: 1:1!25: (null)
exec gdb failed: そのようなファイルやディレクトリはありません
Error: signal Segmentation fault:
cockpit-bridge(+0x439c9)[0x643c9f8439c9]
/lib64/libc.so.6(+0x36400)[0x7e7de0c10400]
/lib64/libglib-2.0.so.0(g_slist_copy_deep+0x80)[0x7e7de1fb2f80]
/lib64/libgobject-2.0.so.0(+0x14441)[0x7e7de2273441]
/lib64/libgobject-2.0.so.0(g_type_class_ref+0x2e6)[0x7e7de228db56]
/lib64/libgobject-2.0.so.0(g_object_new_valist+0x559)[0x7e7de2276399]
/lib64/libgobject-2.0.so.0(g_object_new+0x99)[0x7e7de22764f9]
cockpit-bridge(+0x2cfc2)[0x643c9f82cfc2]
cockpit-bridge(+0x2d39a)[0x643c9f82d39a]
cockpit-bridge(+0x2df49)[0x643c9f82df49]
/lib64/libffi.so.6(ffi_call_unix64+0x4c)[0x7e7de09d7e2c]
/lib64/libffi.so.6(ffi_call+0x1f5)[0x7e7de09d7755]
/lib64/libgobject-2.0.so.0(g_cclosure_marshal_generic+0x1f8)[0x7e7de226f258]
/lib64/libgobject-2.0.so.0(g_closure_invoke+0x138)[0x7e7de226ea18]
/lib64/libgobject-2.0.so.0(+0x220fd)[0x7e7de22810fd]
/lib64/libgobject-2.0.so.0(g_signal_emit_valist+0xafc)[0x7e7de2288d7c]
```

```
bash-4.2# mkdir -p /var/run/dbus
bash-4.2# dbus-daemon --system --fork
bash-4.2# ps aux | grep dbus
dbus         123  0.0  0.0  58116  2952 ?        Ss   07:15   0:00 dbus-daemon --system --fork
root         125  0.0  0.0 114296  2304 pts/1    S+   07:15   0:00 grep dbus
bash-4.2# /usr/libexec/cockpit-ws --no-tls -p 9090
```
とりあえずログインはできるようになった  
* [OK]システム
* [NG]ログ
* [NG]ネットワーキング
* [OK]アカウント
* [NG]サービス
* [NG]Diagnostic Reports
* [NG]SELinux
* [???]カーネルダンプ
* [OK]端末

だいたい以下のエラー  
No journal files were found.