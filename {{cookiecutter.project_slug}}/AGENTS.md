# Agent Instructions

This repository is an Ansible project using Python 3.12.

- Use Ansible modules with fully qualified collection names.
- Keep playbooks idempotent; avoid shell or command tasks when a module exists.
- Never commit credentials, vault passwords, private keys, or plaintext secrets.
- Keep direct Python dependencies pinned in `requirements.txt`; use `requirements.yml` if Galaxy collections or roles are added.
- Before finishing changes, run `ansible-lint playbooks/`, `yamllint playbooks/`, and `ansible-playbook --syntax-check playbooks/site.yml` from the repository root.
- Do not disable lint rules or change unrelated files to make checks pass.
