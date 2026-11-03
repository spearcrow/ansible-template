# Template Repo Ansible

Template Cookiecutter untuk membuat repository Ansible baru dengan Python 3.12, konfigurasi inventory lokal, contoh playbook, dan aturan coding agent di `AGENTS.md`. Cruft dapat dipakai untuk membuat proyek sekaligus melacak pembaruan template.

## Membuat repo baru

Template sudah memiliki commit Git, tetapi belum memiliki remote. Publikasikan repo template terlebih dahulu, lalu jalankan dari direktori tempat repo baru akan dibuat:

```sh
python3.12 -m venv .venv
.venv/bin/python -m pip install cruft==2.16.0 cookiecutter==2.7.1
.venv/bin/cruft create <URL_REPO_TEMPLATE>
```

Ganti `<URL_REPO_TEMPLATE>` dengan URL Git repo template yang sudah dipublikasikan. Isi nama proyek saat diminta; nama direktori mengikuti `project_slug` yang bisa diubah saat prompt. Commit `.cruft.json` yang dihasilkan bersama file proyek agar versi template asal tetap tercatat.

## Memperbarui repo turunan

Setelah perubahan template di-commit dan dipublikasikan, jalankan dari root repo turunan:

```sh
../.venv/bin/cruft check
../.venv/bin/cruft update
```

Tinjau perubahan sebelum menerimanya, terutama pada `playbooks/site.yml` yang mungkin sudah dikustomisasi. Cruft menyinkronkan perubahan template, bukan otomatis menaikkan versi paket dari PyPI. README ini berada di repo template, bukan di repo turunan.

## Menggunakan repo hasil generate

Masuk ke direktori proyek yang baru dibuat, lalu jalankan:

```sh
python3.12 -m venv .venv
.venv/bin/python -m pip install -r requirements.txt
.venv/bin/ansible-galaxy install -r requirements.yml
.venv/bin/ansible-lint playbooks/
.venv/bin/yamllint playbooks/
.venv/bin/ansible-playbook --syntax-check playbooks/site.yml
.venv/bin/ansible-playbook playbooks/site.yml
```

Inventory default menunjuk ke `localhost`. Ubah `inventory/hosts.ini` dan `ansible.cfg` sesuai target sebelum memakai playbook untuk host lain.

## Versi dan struktur

- `requirements-cookiecutter.txt` mengunci Cookiecutter 2.7.1; perintah pembuatan proyek di atas juga mengunci Cruft 2.16.0.
- `requirements.txt` pada hasil generate mengunci Ansible 14.5.0, ansible-core 2.21.6, ansible-lint 26.10.1, dan yamllint 1.38.0.
- `requirements.yml` mencatat role dan collection Galaxy; `ansible.cfg` mengarahkan instalasi ke `roles/` (collection di `roles/ansible_collections/`).
- `.python-version` menyatakan Python 3.12; gunakan interpreter Python 3.12 untuk membuat environment.
- `AGENTS.md` pada hasil generate berisi aturan perubahan dan pemeriksaan untuk coding agent.
- Playbook di `playbooks/` disalin tanpa render agar ekspresi Jinja Ansible tetap utuh.

Hanya dependensi Python langsung yang dikunci; dependensi transitif masih dapat berubah saat instalasi. Daftar role dan collection Galaxy awalnya kosong; tambahkan nama dan versi eksplisit saat dibutuhkan.
