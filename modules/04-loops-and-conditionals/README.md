# Module 4: Loops, Conditionals, and Tags

## What you'll learn
- Create multiple resources using `loop`
- Loop over lists and dictionaries
- Combine `when` conditionals with loops
- Use `block`, `rescue`, and `always` for error handling
- Apply tags for selective task execution

## Playbooks in This Module

| # | Playbook | Concepts Taught |
|---|----------|----------------|
| 1 | `01_loops_basics.yml` | loop, `{{ item }}` |
| 2 | `02_loops_dict.yml` | Looping over dictionaries |
| 3 | `03_conditionals_multi_os.yml` | block + when for OS-specific logic |
| 4 | `04_block_rescue.yml` | block/rescue/always error handling |
| 5 | `05_tags_demo.yml` | Tags for selective execution |

## How to Run

```bash
ansible-playbook modules/04-loops-and-conditionals/01_loops_basics.yml
ansible-playbook modules/04-loops-and-conditionals/05_tags_demo.yml --tags install
ansible-playbook modules/04-loops-and-conditionals/05_tags_demo.yml --skip-tags verify
ansible-playbook modules/04-loops-and-conditionals/05_tags_demo.yml --tags "install,verify"
```

## Good to know
- `loop` replaces the deprecated `with_items` (but both still work)
- Access loop items via `{{ item }}` — for dicts, use `{{ item.key }}`
- `block/rescue/always` is Ansible's try/catch/finally
- Tags let you run subsets of a playbook — great for debugging and selective execution
