# Template Repo Ansible

Template Cookiecutter untuk membuat repository Ansible baru dengan Python 3.12, konfigurasi inventory lokal, contoh playbook, dan aturan coding agent di `AGENTS.md`.

## Membuat repo baru

Jalankan dari direktori template ini:

```sh
python3.12 -m venv .venv
.venv/bin/python -m pip install -r requirements-cookiecutter.txt
.venv/bin/cookiecutter . --output-dir ..
```

Isi nama proyek saat diminta. Cookiecutter membuat direktori baru di direktori induk; nama direktori mengikuti `project_slug` yang bisa diubah saat prompt.

## Menggunakan repo hasil generate

Masuk ke direktori proyek yang baru dibuat, lalu jalankan:

```sh
python3.12 -m venv .venv
.venv/bin/python -m pip install -r requirements.txt
.venv/bin/ansible-lint playbooks/
.venv/bin/yamllint playbooks/
.venv/bin/ansible-playbook --syntax-check playbooks/site.yml
.venv/bin/ansible-playbook playbooks/site.yml
```

Inventory default menunjuk ke `localhost`. Ubah `inventory/hosts.ini` dan `ansible.cfg` sesuai target sebelum memakai playbook untuk host lain.

## Versi dan struktur

- `requirements-cookiecutter.txt` mengunci Cookiecutter 2.7.1 untuk membuat proyek.
- `requirements.txt` pada hasil generate mengunci Ansible 14.5.0, ansible-core 2.21.6, ansible-lint 26.10.1, dan yamllint 1.38.0.
- `.python-version` menyatakan Python 3.12; gunakan interpreter Python 3.12 untuk membuat environment.
- `AGENTS.md` pada hasil generate berisi aturan perubahan dan pemeriksaan untuk coding agent.
- Playbook di `playbooks/` disalin tanpa render agar ekspresi Jinja Ansible tetap utuh.

Hanya dependensi Python langsung yang dikunci; dependensi transitif masih dapat berubah saat instalasi. Jika proyek memerlukan collection atau role dari Ansible Galaxy, tambahkan `requirements.yml` di repo hasil generate.
