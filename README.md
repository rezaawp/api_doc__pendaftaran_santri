# API Spec

## BASE URL

<https://api.rezawp.com/api/v1>

## Standard Format Response

```json
{
    "status": "boolean",
    "message": "string",
    "data": "array"
}
```

If return response status code expect 200, then status = false

## Status Responses

-   200 (OK)
-   401 (Unauthorized)
-   500 (Internal Server Error)
-   404 (Not Found)
-   422 (Error Validations)

## Authentication

All API must use this Request Headers. Except : register, login, me

Request :

-   Headers :
    -   Authorization : Bearer token
    -   Content-Type : application/json
    -   Accept : application/json

## Register

Request :

-   Method : POST
-   Endpoint : `/auth/register`
-   Body :

```json
{
    "name": "required, string, max:255",
    "email": "required, string, email, max:255, unique",
    "password": "required",
    "password_confirmation": "required, same:password_confirmation"
}
```

Response (200) :

```json
{
    "status": true,
    "message": "string",
    "data": {
        "name": "string",
        "email": "string|email",
        "password": "string"
    }
}
```

## Login

Request :

-   Method : POST
-   Endpoint : `/auth/login`
-   Body :

```json
{
    "email": "string|email",
    "password": "string"
}
```

Response (200) :

```json
{
    "status": true,
    "message": "Berhasil Membuat Akun",
    "data": {
        "access_token": "string",
        "token_type": "string",
        "expires_in": "integer"
    }
}
```

## User

Request :

-   Method : POST
-   Endpoint : `/auth/me`

Response (200) :

```json
{
    "status": true,
    "message": "OK",
    "data": {
        "id": "integer",
        "name": "string",
        "email": "string | email",
        "email_verified_at": null,
        "created_at": "timestamps",
        "updated_at": "timestamps",
        "roles": [
            {
                "id": "integer",
                "name": "string",
                "guard_name": "string",
                "created_at": "timestamps",
                "updated_at": "timestamps",
                "pivot": {
                    "model_id": "integer",
                    "role_id": "integer",
                    "model_type": "string | path-model"
                }
            }
        ],
        "santris": [
            {
                "id": "integer",
                "user_id": "integer",
                "nama_lengkap": "string",
                "nama_arab": "string",
                "nama_panggilan": "string",
                "ttl": "2015-04-01",
                "no_ktp": "string",
                "suku": "string",
                "daerah": "string",
                "konsulat": "string",
                "warga_negara": "string",
                "kota_dibesarkan": "string",
                "no_telepon": "string",
                "no_hp": "string",
                "lulusan": "string",
                "tahun_lulus": "integer",
                "no_stambuk": "integer",
                "status": "string",
                "created_at": "timestamps",
                "updated_at": "timestamps"
            }
        ],
        "data_kelas": [
            {
                "id": "integer",
                "user_id": "integer",
                "nama_kelas": "string",
                "kode_kelas": "string",
                "nomor_kelas": "integer",
                "created_at": "timestamps",
                "updated_at": "timestamps"
            }
        ],
        "data_asrama": [
            {
                "id": "integer",
                "user_id": "integer",
                "nama": "string",
                "alamat": "text",
                "pengurus": "json",
                "created_at": "timestamps",
                "updated_at": "timestamps"
            }
        ],
        "data_kamar": [
            {
                "id": "integer",
                "user_id": "integer",
                "data_asrama_id": "integer",
                "kode_kamar": "integer",
                "nama_kamar": "string",
                "created_at": "timestamps",
                "updated_at": "timestamps"
            }
        ],
        "data_staf": [
            {
                "id": "integer",
                "user_id": "integer",
                "kode": "string",
                "nama": "string",
                "nomor_telepon": "string",
                "created_at": "timestamps",
                "updated_at": "timestamps"
            }
        ],
        "data_pelanggaran": [
            {
                "id": "integer",
                "user_id": "integer",
                "santri_id": "integer",
                "jumlah_point": "integer",
                "created_at": "timestamps",
                "updated_at": "timestamps"
            }
        ],
        "aturan_pelanggaran": [
            {
                "id": "integer",
                "user_id": "integer",
                "point": "integer",
                "catatan": "string",
                "hukuman": "string",
                "staf_id": "integer",
                "created_at": "timestamps",
                "updated_at": "timestamps"
            }
        ]
    }
}
```

## Logout

Request :

-   Method : POST
-   Endpoint : `/api/auth/logout`

Response (200) :

```json
{
    "status": "integer",
    "message": "string",
    "data": "array|null"
}
```

# Admin

## Santri

### Store

Request :

-   Method : POST
-   Endpoint : `/admin/santri`
-   Example Body Request :

```json
{
    "nama_lengkap": "asss",
    "nama_arab": "test",
    "nama_panggilan": "test",
    "ttl": "test",
    "no_ktp": "12345",
    "suku": "test",
    "daerah": "test",
    "konsulat": "test",
    "warga_negara": "test",
    "kota_dibesarkan": "test",
    "no_telepon": "123454545",
    "no_hp": "123454545",
    "lulusan": "test",
    "tahun_lulus": "2345"
}
```

Example Response (200) :

```json
{
    "status": true,
    "message": "Success",
    "data": {
        "nama_lengkap": "asss",
        "nama_arab": "test",
        "nama_panggilan": "test",
        "ttl": "test",
        "no_ktp": "12345",
        "suku": "test",
        "daerah": "test",
        "konsulat": "test",
        "warga_negara": "test",
        "kota_dibesarkan": "test",
        "no_telepon": "123454545",
        "no_hp": "123454545",
        "lulusan": "test",
        "tahun_lulus": "2345",
        "user_id": 1,
        "no_stambuk": 1674969557,
        "updated_at": "2023-01-29T05:19:17.000000Z",
        "created_at": "2023-01-29T05:19:17.000000Z",
        "id": 6
    }
}
```

### Show

Request :

-   Method : GET
-   Endpoint : `/admin/santri/{id}`

Response (200) :

```json
{
    "status": true,
    "message": "Success",
    "data": {
        "id": 1,
        "user_id": "integer",
        "nama_lengkap": "string",
        "nama_arab": "string",
        "nama_panggilan": "string",
        "ttl": "2015-04-01",
        "no_ktp": "string",
        "suku": "string",
        "daerah": "string",
        "konsulat": "string",
        "warga_negara": "string",
        "kota_dibesarkan": "string",
        "no_telepon": "string",
        "no_hp": "string",
        "lulusan": "string",
        "tahun_lulus": "integer",
        "no_stambuk": "integer",
        "status": "string",
        "created_at": "timestamps",
        "updated_at": "timestamps",
        "admin": {
            "id": "integer",
            "name": "string",
            "email": "string",
            "email_verified_at": "timestamps",
            "created_at": "timestamps",
            "updated_at": "timestamps"
        },
        "alamat_santri": {
            "id": "int",
            "santri_id": "foreign",
            "kampung": "string",
            "ponpes": "string",
            "jalan": "text",
            "km": "string",
            "gang": "string",
            "perum": "string",
            "blok": "string",
            "no_rumah": "int",
            "rt": "int",
            "rw": "int",
            "dusun": "string",
            "kelurahan": "string",
            "desa": "string",
            "kecamatan": "string",
            "kabupaten": "string",
            "kota": "string",
            "provinsi": "string",
            "kodepos": "string",
            "created_at": "timestamps",
            "updated_at": "timestamps"
        },
        "ayah_santri": {
            "id": "integer",
            "santri_id": "integer",
            "nama_lengkap": "string",
            "nama_arab": "string",
            "usia": "integer",
            "alm": "enum(ya, tidak)",
            "karir": "string",
            "pendidikan": "string",
            "suku": "string",
            "agama": "string",
            "warga_negara": "string",
            "tahun": "integer",
            "alumni_gontor": "enum(ya, tidak)",
            "no_stambuk": "integer",
            "tahun_alumni": "integer",
            "created_at": "timestamps",
            "updated_at": "timestamps"
        },
        "wali_santri": {
            "id": "int",
            "santri_id": "foreign",
            "nama_lengkap": "string",
            "nama_arab": "string",
            "usia": "int",
            "hubungan": "string",
            "karir": "string",
            "pendidikan": "string",
            "suku": "string",
            "agama": "string",
            "warga_negara": "string",
            "tahun": "int",
            "alumni_gontor": "enum(ya, tidak)",
            "no_stambuk": "int",
            "tahun_alumni": "int",
            "created_at": "timestamps",
            "updated_at": "timestamps"
        },
        "ibu_santri": {
            "id": "int",
            "santri_id": "foreign",
            "nama_lengkap": "string",
            "nama_arab": "string",
            "usia": "int",
            "alm": "enum",
            "karir": "string",
            "pendidikan": "string",
            "suku": "string",
            "agama": "string",
            "warga_negara": "string",
            "tahun": "int",
            "alumni_gontor": "enum(ya, tidak)",
            "no_stambuk": "int",
            "tahun_alumni": "int",
            "biaya_min": "int",
            "biaya_max": "int",
            "created_at": "timestamps",
            "updated_at": "timestamps"
        },
        "fisik_santri": {
            "id": "int",
            "santri_id": "foreign",
            "golongan_darah": "enum(a, b, o, ab, tidak tahu)",
            "tinggi_tahun": { "tinggi": "int", "tahun": "int" },
            "berat_tahun": { "berat": "int", "tahun": "int" },
            "pendidikan_rumah": "enum(ketat, sedang, bebas)",
            "ekonomi_keluarga": "enum(mampu, cukup, kurang)",
            "situasi_rumah": "enum(perkotaan, pedesaan, perkampungan)",
            "letak_rumah": "string",
            "khitan": "enum(sudah, belum)",
            "situasi_agama": "enum(baik, sedang, kurang)",
            "mata": "string",
            "kacamata": "string",
            "telinga": "string",
            "operasi": "string",
            "kecelakaan": "string",
            "alergi": "string",
            "penyakit": { "nama": "string", "tahun": "int" },
            "kelainan_fisik": "string",
            "status_penyakit": "enum(ada, tidak)",
            "created_at": "timestamps",
            "updated_at": "timestamps"
        },
        "kecakapan_santri": {
            "id": "int",
            "santri_id": "foreign",
            "olahraga": "string",
            "kesenian": "string",
            "keterampilan": "string",
            "lainnya": "string",
            "created_at": "timestamps",
            "updated_at": "timestamps"
        },
        "kurikuler_santri": {
            "id": "int",
            "santri_id": "foreign",
            "olahraga": "string",
            "bahasa": "string",
            "kesenian": "string",
            "keterampilan": "string",
            "asisten": "string",
            "lainnya": "string",
            "keterangan": "string",
            "created_at": "timestamps",
            "updated_at": "timestamps"
        },
        "pengalaman_santri": {
            "id": "int",
            "santri_id": "foreign",
            "dalam_luar": "string",
            "organisasi_panitia": "string",
            "kepanitian": "string",
            "bagian": "string",
            "tahun": "int",
            "created_at": "timestamps",
            "updated_at": "timestamps"
        },
        "riwayat_kelas_santri": {
            "id": "int",
            "santri_id": "foreign",
            "no_kelas": "int",
            "wali_kelas": "string",
            "tahun_kelas": "int",
            "no_asrama": "int",
            "kamar_asrama": "string",
            "tahun_asrama": "int",
            "created_at": "timestamps",
            "updated_at": "timestamps"
        },
        "saudara_santri": {
            "id": "int",
            "santri_id": "foreign",
            "nama": "string",
            "gender": "string",
            "umur": "int",
            "pendidikan": "string",
            "pekerjaan": "string",
            "status": "string",
            "created_at": "timestamps",
            "updated_at": "timestamps"
        },
        "prestasi_santri": {
            "id": "int",
            "santri_id": "foreign",
            "bidang": "string",
            "juara": "int",
            "tahun": "int",
            "created_at": "timestamps",
            "updated_at": "timestamps"
        },
        "pendidikan_sebelum_santri": {
            "id": "int",
            "santri_id": "foreign",
            "pondok": "string",
            "daerah": "string",
            "tahun": "int",
            "created_at": "timestamps",
            "updated_at": "timestamps"
        },
        "saudara_belajar_santri": {
            "id": "int",
            "santri_id": "int",
            "nama": "string",
            "gender": "string",
            "b_a": "string",
            "kelas": "string",
            "gontor": "string",
            "alumni": "int",
            "created_at": "timestamps",
            "updated_at": "timestamps"
        },
        "saudara_jauh_santri": {
            "id": "int",
            "santri_id": "int",
            "nama": "string",
            "gender": "enum(laki-laki, perempuan)",
            "b_a": "string",
            "kelas": "string",
            "gontor": "string",
            "alumni": "int",
            "created_at": "timestamps",
            "updated_at": "timestamps"
        },
        "kamar_kelas_santri": {
            "id": "int",
            "santri_id": "int",
            "data_kelas_id": "int",
            "no_absen_kelas": "int",
            "data_asrama_id": "int",
            "data_kamar_id": "int",
            "no_absen_kamar": "int",
            "created_at": "timestamps",
            "updated_at": "timestamps",
            "data_kelas": {
                "id": "int",
                "user_id": "int",
                "nama_kelas": "string",
                "kode_kelas": "string",
                "nomor_kelas": "int",
                "created_at": "timestamps",
                "updated_at": "timestamps"
            },
            "data_asrama": {
                "id": "int",
                "user_id": "int",
                "nama": "string",
                "alamat": "text",
                "pengurus": {
                    "nama": "string",
                    "telepon": "string",
                    "email": "string"
                },
                "created_at": "timestamps",
                "updated_at": "timestamps"
            },
            "data_kamar": {
                "id": "int",
                "user_id": "int",
                "data_asrama_id": "int",
                "kode_kamar": "int",
                "nama_kamar": "string",
                "created_at": "timestamps",
                "updated_at": "timestamps"
            }
        },
        "data_pelanggaran": {
            "id": "int",
            "user_id": "int",
            "santri_id": "int",
            "jumlah_point": "int",
            "created_at": "timestamps",
            "updated_at": "timestamps"
        }
    }
}
```

### Show All

```json
{
    "status": true,
    "message": "Success",
    "data": [
        {
            "id": 1,
            "user_id": "integer",
            "nama_lengkap": "string",
            "nama_arab": "string",
            "nama_panggilan": "string",
            "ttl": "2015-04-01",
            "no_ktp": "string",
            "suku": "string",
            "daerah": "string",
            "konsulat": "string",
            "warga_negara": "string",
            "kota_dibesarkan": "string",
            "no_telepon": "string",
            "no_hp": "string",
            "lulusan": "string",
            "tahun_lulus": "integer",
            "no_stambuk": "integer",
            "status": "string",
            "created_at": "timestamps",
            "updated_at": "timestamps",
            "admin": {
                "id": "integer",
                "name": "string",
                "email": "string",
                "email_verified_at": "timestamps",
                "created_at": "timestamps",
                "updated_at": "timestamps"
            },
            "alamat_santri": {
                "id": "int",
                "santri_id": "foreign",
                "kampung": "string",
                "ponpes": "string",
                "jalan": "text",
                "km": "string",
                "gang": "string",
                "perum": "string",
                "blok": "string",
                "no_rumah": "int",
                "rt": "int",
                "rw": "int",
                "dusun": "string",
                "kelurahan": "string",
                "desa": "string",
                "kecamatan": "string",
                "kabupaten": "string",
                "kota": "string",
                "provinsi": "string",
                "kodepos": "string",
                "created_at": "timestamps",
                "updated_at": "timestamps"
            },
            "ayah_santri": {
                "id": "integer",
                "santri_id": "integer",
                "nama_lengkap": "string",
                "nama_arab": "string",
                "usia": "integer",
                "alm": "enum(ya, tidak)",
                "karir": "string",
                "pendidikan": "string",
                "suku": "string",
                "agama": "string",
                "warga_negara": "string",
                "tahun": "integer",
                "alumni_gontor": "enum(ya, tidak)",
                "no_stambuk": "integer",
                "tahun_alumni": "integer",
                "created_at": "timestamps",
                "updated_at": "timestamps"
            },
            "wali_santri": {
                "id": "int",
                "santri_id": "foreign",
                "nama_lengkap": "string",
                "nama_arab": "string",
                "usia": "int",
                "hubungan": "string",
                "karir": "string",
                "pendidikan": "string",
                "suku": "string",
                "agama": "string",
                "warga_negara": "string",
                "tahun": "int",
                "alumni_gontor": "enum(ya, tidak)",
                "no_stambuk": "int",
                "tahun_alumni": "int",
                "created_at": "timestamps",
                "updated_at": "timestamps"
            },
            "ibu_santri": {
                "id": "int",
                "santri_id": "foreign",
                "nama_lengkap": "string",
                "nama_arab": "string",
                "usia": "int",
                "alm": "enum",
                "karir": "string",
                "pendidikan": "string",
                "suku": "string",
                "agama": "string",
                "warga_negara": "string",
                "tahun": "int",
                "alumni_gontor": "enum(ya, tidak)",
                "no_stambuk": "int",
                "tahun_alumni": "int",
                "biaya_min": "int",
                "biaya_max": "int",
                "created_at": "timestamps",
                "updated_at": "timestamps"
            },
            "fisik_santri": {
                "id": "int",
                "santri_id": "foreign",
                "golongan_darah": "enum(a, b, o, ab, tidak tahu)",
                "tinggi_tahun": { "tinggi": "int", "tahun": "int" },
                "berat_tahun": { "berat": "int", "tahun": "int" },
                "pendidikan_rumah": "enum(ketat, sedang, bebas)",
                "ekonomi_keluarga": "enum(mampu, cukup, kurang)",
                "situasi_rumah": "enum(perkotaan, pedesaan, perkampungan)",
                "letak_rumah": "string",
                "khitan": "enum(sudah, belum)",
                "situasi_agama": "enum(baik, sedang, kurang)",
                "mata": "string",
                "kacamata": "string",
                "telinga": "string",
                "operasi": "string",
                "kecelakaan": "string",
                "alergi": "string",
                "penyakit": { "nama": "string", "tahun": "int" },
                "kelainan_fisik": "string",
                "status_penyakit": "enum(ada, tidak)",
                "created_at": "timestamps",
                "updated_at": "timestamps"
            },
            "kecakapan_santri": {
                "id": "int",
                "santri_id": "foreign",
                "olahraga": "string",
                "kesenian": "string",
                "keterampilan": "string",
                "lainnya": "string",
                "created_at": "timestamps",
                "updated_at": "timestamps"
            },
            "kurikuler_santri": {
                "id": "int",
                "santri_id": "foreign",
                "olahraga": "string",
                "bahasa": "string",
                "kesenian": "string",
                "keterampilan": "string",
                "asisten": "string",
                "lainnya": "string",
                "keterangan": "string",
                "created_at": "timestamps",
                "updated_at": "timestamps"
            },
            "pengalaman_santri": {
                "id": "int",
                "santri_id": "foreign",
                "dalam_luar": "string",
                "organisasi_panitia": "string",
                "kepanitian": "string",
                "bagian": "string",
                "tahun": "int",
                "created_at": "timestamps",
                "updated_at": "timestamps"
            },
            "riwayat_kelas_santri": {
                "id": "int",
                "santri_id": "foreign",
                "no_kelas": "int",
                "wali_kelas": "string",
                "tahun_kelas": "int",
                "no_asrama": "int",
                "kamar_asrama": "string",
                "tahun_asrama": "int",
                "created_at": "timestamps",
                "updated_at": "timestamps"
            },
            "saudara_santri": {
                "id": "int",
                "santri_id": "foreign",
                "nama": "string",
                "gender": "string",
                "umur": "int",
                "pendidikan": "string",
                "pekerjaan": "string",
                "status": "string",
                "created_at": "timestamps",
                "updated_at": "timestamps"
            },
            "prestasi_santri": {
                "id": "int",
                "santri_id": "foreign",
                "bidang": "string",
                "juara": "int",
                "tahun": "int",
                "created_at": "timestamps",
                "updated_at": "timestamps"
            },
            "pendidikan_sebelum_santri": {
                "id": "int",
                "santri_id": "foreign",
                "pondok": "string",
                "daerah": "string",
                "tahun": "int",
                "created_at": "timestamps",
                "updated_at": "timestamps"
            },
            "saudara_belajar_santri": {
                "id": "int",
                "santri_id": "int",
                "nama": "string",
                "gender": "string",
                "b_a": "string",
                "kelas": "string",
                "gontor": "string",
                "alumni": "int",
                "created_at": "timestamps",
                "updated_at": "timestamps"
            },
            "saudara_jauh_santri": {
                "id": "int",
                "santri_id": "int",
                "nama": "string",
                "gender": "enum(laki-laki, perempuan)",
                "b_a": "string",
                "kelas": "string",
                "gontor": "string",
                "alumni": "int",
                "created_at": "timestamps",
                "updated_at": "timestamps"
            },
            "kamar_kelas_santri": {
                "id": "int",
                "santri_id": "int",
                "data_kelas_id": "int",
                "no_absen_kelas": "int",
                "data_asrama_id": "int",
                "data_kamar_id": "int",
                "no_absen_kamar": "int",
                "created_at": "timestamps",
                "updated_at": "timestamps",
                "data_kelas": {
                    "id": "int",
                    "user_id": "int",
                    "nama_kelas": "string",
                    "kode_kelas": "string",
                    "nomor_kelas": "int",
                    "created_at": "timestamps",
                    "updated_at": "timestamps"
                },
                "data_asrama": {
                    "id": "int",
                    "user_id": "int",
                    "nama": "string",
                    "alamat": "text",
                    "pengurus": {
                        "nama": "string",
                        "telepon": "string",
                        "email": "string"
                    },
                    "created_at": "timestamps",
                    "updated_at": "timestamps"
                },
                "data_kamar": {
                    "id": "int",
                    "user_id": "int",
                    "data_asrama_id": "int",
                    "kode_kamar": "int",
                    "nama_kamar": "string",
                    "created_at": "timestamps",
                    "updated_at": "timestamps"
                }
            },
            "data_pelanggaran": {
                "id": "int",
                "user_id": "int",
                "santri_id": "int",
                "jumlah_point": "int",
                "created_at": "timestamps",
                "updated_at": "timestamps"
            }
        }
    ]
}
```

For Detail, Please Contact Me From <https://rezawp.com/#section_5>

All responses based on database design
