# Copyright (C) 2015 Google Inc.
# All rights reserved.
#
# Redistribution and use in source and binary forms, with or without
# modification, are permitted provided that the following conditions
# are met:
# 1. Redistributions of source code must retain the above copyright
#    notice, this list of conditions and the following disclaimer.
# 2. Redistributions in binary form must reproduce the above copyright
#    notice, this list of conditions and the following disclaimer in the
#    documentation and/or other materials provided with the distribution.
#
# THIS SOFTWARE IS PROVIDED BY THE AUTHOR AND CONTRIBUTORS ``AS IS'' AND
# ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE
# IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE
# ARE DISCLAIMED.  IN NO EVENT SHALL THE AUTHOR OR CONTRIBUTORS BE LIABLE
# FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL
# DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS
# OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION)
# HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT
# LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY
# OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF
# SUCH DAMAGE.

licenses(["notice"])  # BSD license

exports_files(["LICENSE"])

package(
    default_visibility = [
        "//visibility:public",
    ],
)

config_setting(
    name = "debug",
    values = {
        "compilation_mode": "dbg",
    },
)

config_setting(
    name = "darwin",
    values = {
        "cpu": "darwin",
    },
)

config_setting(
    name = "freebsd",
    values = {
        "cpu": "freebsd",
    },
)

genrule(
    name = "configure",
    srcs = [
        "auto/cc/clang",
        "auto/cc/conf",
        "auto/cc/gcc",
        "auto/cc/name",
        "auto/configure",
        "auto/define",
        "auto/endianness",
        "auto/feature",
        "auto/have",
        "auto/have_headers",
        "auto/headers",
        "auto/include",
        "auto/init",
        "auto/install",
        "auto/lib/conf",
        "auto/lib/make",
        "auto/make",
        "auto/module",
        "auto/modules",
        "auto/nohave",
        "auto/options",
        "auto/os/conf",
        "auto/sources",
        "auto/stubs",
        "auto/summary",
        "auto/threads",
        "auto/types/sizeof",
        "auto/types/typedef",
        "auto/types/uintptr_t",
        "auto/types/value",
        "auto/unix",
    ] + select({
        ":darwin": [
            "auto/os/darwin",
        ],
        ":freebsd": [
            "auto/os/freebsd",
        ],
        "//conditions:default": [
            "auto/os/linux",
        ],
    }),
    outs = [
        "objs/autoconf.err",
        "objs/autoconf.log",
        "objs/ngx_auto_config.h",
        "objs/ngx_auto_headers.h",
    ],
    cmd = "$(location auto/configure)" +
          " --builddir=\"$(@D)/objs\"" +
          " --with-cc=\"$(CC)\"" +
          " --with-cc-opt=\"$(CC_FLAGS)\"" +
          " --with-ipv6" +
          " --without-http" +
          " --without-http-cache" +
          " --without-http_auth_basic_module" +
          " --without-http_upstream_zone_module" +
          " 2>&1 >$(@D)/objs/autoconf.log",
    visibility = [
        "//visibility:private",
    ],
)

cc_library(
    name = "core",
    srcs = [
        "objs/ngx_auto_config.h",
        "objs/ngx_auto_headers.h",
        "src/core/nginx.c",
        "src/core/ngx_array.c",
        "src/core/ngx_array.h",
        "src/core/ngx_buf.c",
        "src/core/ngx_buf.h",
        "src/core/ngx_conf_file.c",
        "src/core/ngx_conf_file.h",
        "src/core/ngx_connection.c",
        "src/core/ngx_connection.h",
        "src/core/ngx_cpuinfo.c",
        "src/core/ngx_crc32.c",
        "src/core/ngx_crc32.h",
        "src/core/ngx_crypt.c",
        "src/core/ngx_cycle.c",
        "src/core/ngx_cycle.h",
        "src/core/ngx_file.c",
        "src/core/ngx_file.h",
        "src/core/ngx_hash.c",
        "src/core/ngx_hash.h",
        "src/core/ngx_inet.c",
        "src/core/ngx_inet.h",
        "src/core/ngx_list.c",
        "src/core/ngx_list.h",
        "src/core/ngx_log.c",
        "src/core/ngx_log.h",
        "src/core/ngx_module.c",
        "src/core/ngx_module.h",
        "src/core/ngx_murmurhash.c",
        "src/core/ngx_murmurhash.h",
        "src/core/ngx_open_file_cache.c",
        "src/core/ngx_open_file_cache.h",
        "src/core/ngx_output_chain.c",
        "src/core/ngx_palloc.c",
        "src/core/ngx_palloc.h",
        "src/core/ngx_parse.c",
        "src/core/ngx_parse.h",
        "src/core/ngx_parse_time.c",
        "src/core/ngx_parse_time.h",
        "src/core/ngx_proxy_protocol.c",
        "src/core/ngx_proxy_protocol.h",
        "src/core/ngx_queue.c",
        "src/core/ngx_queue.h",
        "src/core/ngx_radix_tree.c",
        "src/core/ngx_radix_tree.h",
        "src/core/ngx_rbtree.c",
        "src/core/ngx_rbtree.h",
        "src/core/ngx_regex.c",
        "src/core/ngx_regex.h",
        "src/core/ngx_resolver.c",
        "src/core/ngx_resolver.h",
        "src/core/ngx_rwlock.c",
        "src/core/ngx_rwlock.h",
        "src/core/ngx_shmtx.c",
        "src/core/ngx_shmtx.h",
        "src/core/ngx_slab.c",
        "src/core/ngx_slab.h",
        "src/core/ngx_spinlock.c",
        "src/core/ngx_string.c",
        "src/core/ngx_string.h",
        "src/core/ngx_syslog.c",
        "src/core/ngx_syslog.h",
        "src/core/ngx_times.c",
        "src/core/ngx_times.h",
        "src/event/ngx_event.c",
        "src/event/ngx_event_accept.c",
        "src/event/ngx_event_connect.c",
        "src/event/ngx_event_openssl.c",
        "src/event/ngx_event_openssl.h",
        "src/event/ngx_event_openssl_stapling.c",
        "src/event/ngx_event_pipe.c",
        "src/event/ngx_event_posted.c",
        "src/event/ngx_event_posted.h",
        "src/event/ngx_event_timer.c",
        "src/event/ngx_event_timer.h",
        "src/os/unix/ngx_alloc.c",
        "src/os/unix/ngx_alloc.h",
        "src/os/unix/ngx_atomic.h",
        "src/os/unix/ngx_channel.c",
        "src/os/unix/ngx_channel.h",
        "src/os/unix/ngx_daemon.c",
        "src/os/unix/ngx_dlopen.c",
        "src/os/unix/ngx_dlopen.h",
        "src/os/unix/ngx_errno.c",
        "src/os/unix/ngx_errno.h",
        "src/os/unix/ngx_files.c",
        "src/os/unix/ngx_files.h",
        "src/os/unix/ngx_os.h",
        "src/os/unix/ngx_posix_init.c",
        "src/os/unix/ngx_process.c",
        "src/os/unix/ngx_process.h",
        "src/os/unix/ngx_process_cycle.c",
        "src/os/unix/ngx_process_cycle.h",
        "src/os/unix/ngx_readv_chain.c",
        "src/os/unix/ngx_recv.c",
        "src/os/unix/ngx_send.c",
        "src/os/unix/ngx_setaffinity.h",
        "src/os/unix/ngx_setproctitle.c",
        "src/os/unix/ngx_setproctitle.h",
        "src/os/unix/ngx_shmem.c",
        "src/os/unix/ngx_shmem.h",
        "src/os/unix/ngx_socket.c",
        "src/os/unix/ngx_socket.h",
        "src/os/unix/ngx_thread.h",
        "src/os/unix/ngx_time.c",
        "src/os/unix/ngx_time.h",
        "src/os/unix/ngx_udp_recv.c",
        "src/os/unix/ngx_user.c",
        "src/os/unix/ngx_user.h",
        "src/os/unix/ngx_writev_chain.c",
    ] + select({
        ":darwin": [
            "src/event/modules/ngx_kqueue_module.c",
            "src/os/unix/ngx_darwin.h",
            "src/os/unix/ngx_darwin_config.h",
            "src/os/unix/ngx_darwin_init.c",
            "src/os/unix/ngx_darwin_sendfile_chain.c",
        ],
        ":freebsd": [
            "src/event/modules/ngx_kqueue_module.c",
            "src/os/unix/ngx_freebsd.h",
            "src/os/unix/ngx_freebsd_config.h",
            "src/os/unix/ngx_freebsd_init.c",
            "src/os/unix/ngx_freebsd_sendfile_chain.c",
            "src/os/unix/ngx_setaffinity.c",
        ],
        "//conditions:default": [
            "src/event/modules/ngx_epoll_module.c",
            "src/os/unix/ngx_linux.h",
            "src/os/unix/ngx_linux_config.h",
            "src/os/unix/ngx_linux_init.c",
            "src/os/unix/ngx_linux_sendfile_chain.c",
            "src/os/unix/ngx_setaffinity.c",
        ],
    }),
    hdrs = [
        "src/core/nginx.h",
        "src/core/ngx_config.h",
        "src/core/ngx_core.h",
        "src/core/ngx_crypt.h",
        "src/core/ngx_md5.h",
        "src/core/ngx_sha1.h",
        "src/event/ngx_event.h",
        "src/event/ngx_event_connect.h",
        "src/event/ngx_event_pipe.h",
    ],
    defines = [
        "NGX_CRYPT",
        "NGX_MODULES",
        "NGX_STAT_STUB",
        # BoringSSL
        "NGX_HAVE_MD5",
        "NGX_HAVE_OPENSSL_MD5_H",
        "NGX_HAVE_SHA1",
        "NGX_HAVE_OPENSSL_SHA1_H",
        "NGX_OPENSSL",
        "NGX_SSL",
        # PCRE
        "NGX_HAVE_PCRE_JIT",
        "NGX_PCRE",
    ] + select({
        ":debug": [
            "NGX_DEBUG",
        ],
        "//conditions:default": [],
    }),
    includes = [
        "objs",
        "src/core",
        "src/event",
        "src/os/unix",
    ],
    linkopts = select({
        ":darwin": [],
        ":freebsd": [
            "-lcrypt",
        ],
        "//conditions:default": [
            "-lcrypt",
            "-ldl",
            "-lpthread",
        ],
    }),
    deps = [
        "//external:boringssl",
        "//external:pcre",
    ],
)

cc_library(
    name = "http",
    srcs = [
        "src/http/modules/ngx_http_chunked_filter_module.c",
        "src/http/modules/ngx_http_headers_filter_module.c",
        "src/http/modules/ngx_http_index_module.c",
        "src/http/modules/ngx_http_log_module.c",
        "src/http/modules/ngx_http_not_modified_filter_module.c",
        "src/http/modules/ngx_http_range_filter_module.c",
        "src/http/modules/ngx_http_ssl_module.c",
        "src/http/modules/ngx_http_ssl_module.h",
        "src/http/modules/ngx_http_static_module.c",
        "src/http/modules/ngx_http_upstream_zone_module.c",
        "src/http/ngx_http.c",
        "src/http/ngx_http_cache.h",
        "src/http/ngx_http_config.h",
        "src/http/ngx_http_copy_filter_module.c",
        "src/http/ngx_http_core_module.c",
        "src/http/ngx_http_core_module.h",
        "src/http/ngx_http_file_cache.c",
        "src/http/ngx_http_header_filter_module.c",
        "src/http/ngx_http_parse.c",
        "src/http/ngx_http_request.c",
        "src/http/ngx_http_request.h",
        "src/http/ngx_http_request_body.c",
        "src/http/ngx_http_script.c",
        "src/http/ngx_http_script.h",
        "src/http/ngx_http_special_response.c",
        "src/http/ngx_http_upstream.c",
        "src/http/ngx_http_upstream.h",
        "src/http/ngx_http_upstream_round_robin.c",
        "src/http/ngx_http_upstream_round_robin.h",
        "src/http/ngx_http_variables.c",
        "src/http/ngx_http_variables.h",
        "src/http/ngx_http_write_filter_module.c",
        "src/http/v2/ngx_http_v2.c",
        "src/http/v2/ngx_http_v2.h",
        "src/http/v2/ngx_http_v2_filter_module.c",
        "src/http/v2/ngx_http_v2_huff_decode.c",
        "src/http/v2/ngx_http_v2_huff_encode.c",
        "src/http/v2/ngx_http_v2_module.c",
        "src/http/v2/ngx_http_v2_module.h",
        "src/http/v2/ngx_http_v2_table.c",
    ],
    hdrs = [
        "src/http/ngx_http.h",
    ],
    defines = [
        "NGX_HTTP",
        "NGX_HTTP_CACHE",
        "NGX_HTTP_GZIP",
        "NGX_HTTP_SSL",
        "NGX_HTTP_UPSTREAM_ZONE",
        "NGX_HTTP_V2",
        "NGX_ZLIB",
    ],
    includes = [
        "src/http",
        "src/http/modules",
        "src/http/v2",
    ],
    deps = [
        ":core",
        "//external:zlib",
    ],
)

cc_library(
    name = "http_access",
    srcs = [
        "src/http/modules/ngx_http_access_module.c",
    ],
    defines = [
        "NGX_HTTP_ACCESS",
    ],
    deps = [
        ":http",
    ],
)

cc_library(
    name = "http_addition",
    srcs = [
        "src/http/modules/ngx_http_addition_filter_module.c",
    ],
    defines = [
        "NGX_HTTP_ADDITION",
    ],
    deps = [
        ":http_postpone",
    ],
)

cc_library(
    name = "http_auth_basic",
    srcs = [
        "src/http/modules/ngx_http_auth_basic_module.c",
    ],
    defines = [
        "NGX_HTTP_AUTH_BASIC",
    ],
    deps = [
        ":http",
    ],
)

cc_library(
    name = "http_auth_request",
    srcs = [
        "src/http/modules/ngx_http_auth_request_module.c",
    ],
    defines = [
        "NGX_HTTP_AUTH_REQUEST",
    ],
    deps = [
        ":http",
    ],
)

cc_library(
    name = "http_autoindex",
    srcs = [
        "src/http/modules/ngx_http_autoindex_module.c",
    ],
    defines = [
        "NGX_HTTP_AUTOINDEX",
    ],
    deps = [
        ":http",
    ],
)

cc_library(
    name = "http_browser",
    srcs = [
        "src/http/modules/ngx_http_browser_module.c",
    ],
    defines = [
        "NGX_HTTP_BROWSER",
    ],
    deps = [
        ":http",
    ],
)

cc_library(
    name = "http_charset",
    srcs = [
        "src/http/modules/ngx_http_charset_filter_module.c",
    ],
    defines = [
        "NGX_HTTP_CHARSET",
    ],
    deps = [
        ":http",
    ],
)

cc_library(
    name = "http_dav",
    srcs = [
        "src/http/modules/ngx_http_dav_module.c",
    ],
    defines = [
        "NGX_HTTP_DAV",
    ],
    deps = [
        ":http",
    ],
)

cc_library(
    name = "http_empty_gif",
    srcs = [
        "src/http/modules/ngx_http_empty_gif_module.c",
    ],
    defines = [
        "NGX_HTTP_EMPTY_GIF",
    ],
    deps = [
        ":http",
    ],
)

cc_library(
    name = "http_fastcgi",
    srcs = [
        "src/http/modules/ngx_http_fastcgi_module.c",
    ],
    defines = [
        "NGX_HTTP_FASTCGI",
    ],
    deps = [
        ":http",
    ],
)

cc_library(
    name = "http_flv",
    srcs = [
        "src/http/modules/ngx_http_flv_module.c",
    ],
    defines = [
        "NGX_HTTP_FLV",
    ],
    deps = [
        ":http",
    ],
)

cc_library(
    name = "http_geo",
    srcs = [
        "src/http/modules/ngx_http_geo_module.c",
    ],
    defines = [
        "NGX_HTTP_GEO",
    ],
    deps = [
        ":http",
    ],
)

cc_library(
    name = "http_gunzip",
    srcs = [
        "src/http/modules/ngx_http_gunzip_filter_module.c",
    ],
    defines = [
        "NGX_HTTP_GUNZIP",
    ],
    deps = [
        ":http",
    ],
)

cc_library(
    name = "http_gzip_filter",
    srcs = [
        "src/http/modules/ngx_http_gzip_filter_module.c",
    ],
    defines = [
        "NGX_HTTP_GZIP_FILTER",
    ],
    deps = [
        ":http",
    ],
)

cc_library(
    name = "http_gzip_static",
    srcs = [
        "src/http/modules/ngx_http_gzip_static_module.c",
    ],
    defines = [
        "NGX_HTTP_GZIP_STATIC",
    ],
    deps = [
        ":http",
    ],
)

cc_library(
    name = "http_limit_conn",
    srcs = [
        "src/http/modules/ngx_http_limit_conn_module.c",
    ],
    defines = [
        "NGX_HTTP_LIMIT_CONN",
    ],
    deps = [
        ":http",
    ],
)

cc_library(
    name = "http_limit_req",
    srcs = [
        "src/http/modules/ngx_http_limit_req_module.c",
    ],
    defines = [
        "NGX_HTTP_LIMIT_REQ",
    ],
    deps = [
        ":http",
    ],
)

cc_library(
    name = "http_map",
    srcs = [
        "src/http/modules/ngx_http_map_module.c",
    ],
    defines = [
        "NGX_HTTP_MAP",
    ],
    deps = [
        ":http",
    ],
)

cc_library(
    name = "http_memcached",
    srcs = [
        "src/http/modules/ngx_http_memcached_module.c",
    ],
    defines = [
        "NGX_HTTP_MEMCACHED",
    ],
    deps = [
        ":http",
    ],
)

cc_library(
    name = "http_mp4",
    srcs = [
        "src/http/modules/ngx_http_mp4_module.c",
    ],
    defines = [
        "NGX_HTTP_MP4",
    ],
    deps = [
        ":http",
    ],
)

cc_library(
    name = "http_postpone",
    srcs = [
        "src/http/ngx_http_postpone_filter_module.c",
    ],
    defines = [
        "NGX_HTTP_POSTPONE",
    ],
    deps = [
        ":http",
    ],
)

cc_library(
    name = "http_proxy",
    srcs = [
        "src/http/modules/ngx_http_proxy_module.c",
    ],
    defines = [
        "NGX_HTTP_PROXY",
    ],
    deps = [
        ":http",
    ],
)

cc_library(
    name = "http_random_index",
    srcs = [
        "src/http/modules/ngx_http_random_index_module.c",
    ],
    defines = [
        "NGX_HTTP_RANDOM_INDEX",
    ],
    deps = [
        ":http",
    ],
)

cc_library(
    name = "http_realip",
    srcs = [
        "src/http/modules/ngx_http_realip_module.c",
    ],
    defines = [
        "NGX_HTTP_REALIP",
    ],
    deps = [
        ":http",
    ],
)

cc_library(
    name = "http_referer",
    srcs = [
        "src/http/modules/ngx_http_referer_module.c",
    ],
    defines = [
        "NGX_HTTP_REFERER",
    ],
    deps = [
        ":http",
    ],
)

cc_library(
    name = "http_rewrite",
    srcs = [
        "src/http/modules/ngx_http_rewrite_module.c",
    ],
    defines = [
        "NGX_HTTP_REWRITE",
    ],
    deps = [
        ":http",
    ],
)

cc_library(
    name = "http_scgi",
    srcs = [
        "src/http/modules/ngx_http_scgi_module.c",
    ],
    defines = [
        "NGX_HTTP_SCGI",
    ],
    deps = [
        ":http",
    ],
)

cc_library(
    name = "http_secure_link",
    srcs = [
        "src/http/modules/ngx_http_secure_link_module.c",
    ],
    defines = [
        "NGX_HTTP_SECURE_LINK",
    ],
    deps = [
        ":http",
    ],
)

cc_library(
    name = "http_slice",
    srcs = [
        "src/http/modules/ngx_http_slice_filter_module.c",
    ],
    defines = [
        "NGX_HTTP_SLICE",
    ],
    deps = [
        ":http_postpone",
    ],
)

cc_library(
    name = "http_split_clients",
    srcs = [
        "src/http/modules/ngx_http_split_clients_module.c",
    ],
    defines = [
        "NGX_HTTP_SPLIT_CLIENTS",
    ],
    deps = [
        ":http",
    ],
)

cc_library(
    name = "http_ssi",
    srcs = [
        "src/http/modules/ngx_http_ssi_filter_module.c",
        "src/http/modules/ngx_http_ssi_filter_module.h",
    ],
    defines = [
        "NGX_HTTP_SSI",
    ],
    deps = [
        ":http_postpone",
    ],
)

cc_library(
    name = "http_stub_status",
    srcs = [
        "src/http/modules/ngx_http_stub_status_module.c",
    ],
    defines = [
        "NGX_HTTP_STUB_STATUS",
    ],
    deps = [
        ":http",
    ],
)

cc_library(
    name = "http_sub",
    srcs = [
        "src/http/modules/ngx_http_sub_filter_module.c",
    ],
    defines = [
        "NGX_HTTP_SUB",
    ],
    deps = [
        ":http",
    ],
)

cc_library(
    name = "http_upstream_hash",
    srcs = [
        "src/http/modules/ngx_http_upstream_hash_module.c",
    ],
    defines = [
        "NGX_HTTP_UPSTREAM_HASH",
    ],
    deps = [
        ":http",
    ],
)

cc_library(
    name = "http_upstream_ip_hash",
    srcs = [
        "src/http/modules/ngx_http_upstream_ip_hash_module.c",
    ],
    defines = [
        "NGX_HTTP_UPSTREAM_IP_HASH",
    ],
    deps = [
        ":http",
    ],
)

cc_library(
    name = "http_upstream_keepalive",
    srcs = [
        "src/http/modules/ngx_http_upstream_keepalive_module.c",
    ],
    defines = [
        "NGX_HTTP_UPSTREAM_KEEPALIVE",
    ],
    deps = [
        ":http",
    ],
)

cc_library(
    name = "http_upstream_least_conn",
    srcs = [
        "src/http/modules/ngx_http_upstream_least_conn_module.c",
    ],
    defines = [
        "NGX_HTTP_UPSTREAM_LEAST_CONN",
    ],
    deps = [
        ":http",
    ],
)

cc_library(
    name = "http_userid",
    srcs = [
        "src/http/modules/ngx_http_userid_filter_module.c",
    ],
    defines = [
        "NGX_HTTP_USERID",
    ],
    deps = [
        ":http",
    ],
)

cc_library(
    name = "http_uwsgi",
    srcs = [
        "src/http/modules/ngx_http_uwsgi_module.c",
    ],
    defines = [
        "NGX_HTTP_UWSGI",
    ],
    deps = [
        ":http",
    ],
)

cc_library(
    name = "mail",
    srcs = [
        "src/mail/ngx_mail.c",
        "src/mail/ngx_mail_auth_http_module.c",
        "src/mail/ngx_mail_core_module.c",
        "src/mail/ngx_mail_handler.c",
        "src/mail/ngx_mail_proxy_module.c",
        "src/mail/ngx_mail_ssl_module.c",
        "src/mail/ngx_mail_ssl_module.h",
    ],
    hdrs = [
        "src/mail/ngx_mail.h",
    ],
    defines = [
        "NGX_MAIL",
        "NGX_MAIL_SSL",
    ],
    includes = [
        "src/mail",
    ],
    deps = [
        ":core",
    ],
)

cc_library(
    name = "mail_parse",
    srcs = [
        "src/mail/ngx_mail_parse.c",
    ],
    hdrs = [
        "src/mail/ngx_mail_imap_module.h",
        "src/mail/ngx_mail_pop3_module.h",
        "src/mail/ngx_mail_smtp_module.h",
    ],
    deps = [
        ":mail",
    ],
)

cc_library(
    name = "mail_imap",
    srcs = [
        "src/mail/ngx_mail_imap_handler.c",
        "src/mail/ngx_mail_imap_module.c",
    ],
    defines = [
        "NGX_MAIL_IMAP",
    ],
    deps = [
        ":mail_parse",
    ],
)

cc_library(
    name = "mail_pop3",
    srcs = [
        "src/mail/ngx_mail_pop3_handler.c",
        "src/mail/ngx_mail_pop3_module.c",
    ],
    defines = [
        "NGX_MAIL_POP3",
    ],
    deps = [
        ":mail_parse",
    ],
)

cc_library(
    name = "mail_smtp",
    srcs = [
        "src/mail/ngx_mail_smtp_handler.c",
        "src/mail/ngx_mail_smtp_module.c",
    ],
    defines = [
        "NGX_MAIL_SMTP",
    ],
    deps = [
        ":mail_parse",
    ],
)

cc_library(
    name = "stream",
    srcs = [
        "src/stream/ngx_stream.c",
        "src/stream/ngx_stream_core_module.c",
        "src/stream/ngx_stream_handler.c",
        "src/stream/ngx_stream_proxy_module.c",
        "src/stream/ngx_stream_ssl_module.c",
        "src/stream/ngx_stream_ssl_module.h",
        "src/stream/ngx_stream_upstream.c",
        "src/stream/ngx_stream_upstream.h",
        "src/stream/ngx_stream_upstream_round_robin.c",
        "src/stream/ngx_stream_upstream_round_robin.h",
        "src/stream/ngx_stream_upstream_zone_module.c",
    ],
    hdrs = [
        "src/stream/ngx_stream.h",
    ],
    defines = [
        "NGX_STREAM",
        "NGX_STREAM_SSL",
        "NGX_STREAM_UPSTREAM_ZONE",
    ],
    includes = [
        "src/stream",
    ],
    deps = [
        ":core",
    ],
)

cc_library(
    name = "stream_access",
    srcs = [
        "src/stream/ngx_stream_access_module.c",
    ],
    defines = [
        "NGX_STREAM_ACCESS",
    ],
    deps = [
        ":stream",
    ],
)

cc_library(
    name = "stream_limit_conn",
    srcs = [
        "src/stream/ngx_stream_limit_conn_module.c",
    ],
    defines = [
        "NGX_STREAM_LIMIT_CONN",
    ],
    deps = [
        ":stream",
    ],
)

cc_library(
    name = "stream_upstream_hash",
    srcs = [
        "src/stream/ngx_stream_upstream_hash_module.c",
    ],
    defines = [
        "NGX_STREAM_UPSTREAM_HASH",
    ],
    deps = [
        ":stream",
    ],
)

cc_library(
    name = "stream_upstream_least_conn",
    srcs = [
        "src/stream/ngx_stream_upstream_least_conn_module.c",
    ],
    defines = [
        "NGX_STREAM_UPSTREAM_LEAST_CONN",
    ],
    deps = [
        ":stream",
    ],
)

filegroup(
    name = "modules",
    srcs = [
        "src/ngx_modules.c",
    ],
)

cc_binary(
    name = "nginx",
    srcs = [
        ":modules",
    ],
    linkstatic = 1,
    deps = [
        ":http",
        ":http_access",
        ":http_addition",
        ":http_auth_basic",
        ":http_auth_request",
        ":http_autoindex",
        ":http_browser",
        ":http_charset",
        ":http_dav",
        ":http_empty_gif",
        ":http_fastcgi",
        ":http_flv",
        ":http_geo",
        ":http_gunzip",
        ":http_gzip_filter",
        ":http_gzip_static",
        ":http_limit_conn",
        ":http_limit_req",
        ":http_map",
        ":http_memcached",
        ":http_mp4",
        ":http_proxy",
        ":http_random_index",
        ":http_realip",
        ":http_referer",
        ":http_rewrite",
        ":http_scgi",
        ":http_secure_link",
        ":http_slice",
        ":http_split_clients",
        ":http_ssi",
        ":http_stub_status",
        ":http_sub",
        ":http_upstream_hash",
        ":http_upstream_ip_hash",
        ":http_upstream_keepalive",
        ":http_upstream_least_conn",
        ":http_userid",
        ":http_uwsgi",
        ":mail",
        ":mail_imap",
        ":mail_pop3",
        ":mail_smtp",
        ":stream",
        ":stream_access",
        ":stream_limit_conn",
        ":stream_upstream_hash",
        ":stream_upstream_least_conn",
    ],
)
