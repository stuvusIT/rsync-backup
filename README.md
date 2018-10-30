# rsync-backup

This role deploys a systemd service that backs up a (possibly remote) filesystem using `rsync`.

## Requirements

Debian

## Role Variables

By default, this role deletes anything in the target tree that is not in the origin tree, in order to make use of filesystem-level snapshots on the target.
**Therefore it is highly suggested to carefully read the default flags of this role before executing it.**

| Variable                    | Default                                      | Description                                                                                                                  |
|:----------------------------|:---------------------------------------------|:-----------------------------------------------------------------------------------------------------------------------------|
| `rsync_backup_source_paths` | `['/', '/boot']`                             | List of source paths that needs to be backed up                                                                              |
| `rsync_backup_target_path`  | `/mnt/backup`                                | Destination path to backup to                                                                                                |
| `rsync_backup_mount_pre`    | `True`                                       | Whether to mount the target path before rsyncing (implies that there has to be a entry for it in `/etc/fstab`)               |
| `rsync_backup_umount_post`  | `True`                                       | Whether to unmount the target path after rsyncing (implies that there has to be a entry for it in `/etc/fstab`)              |
| `rsync_backup_flags`        | _see [defaults/main.yml](defaults/main.yml)_ | A list of flags to set when executing rsync, like `delete-during` or `stats`                                                 |
| `rsync_backup_short_flags`  | _see [defaults/main.yml](defaults/main.yml)_ | A list of single-char flags to set when executing rsync, like `a` or `h`                                                     |
| `rsync_backup_excludes`     | _see [defaults/main.yml](defaults/main.yml)_ | A list of paths to exclude from backing up. Paths are relative to the source and target paths if they don't start with a `/` |
| `rsync_backup_frequency`    | `daily`                                      | systemd execution frequency of the timer                                                                                     |

## Example Playbook

```yml
- hosts: backup_client
  roles:
    - role: rsync-backup
      rsync_backup_target_path: /mnt/mybackup
```

## License

This work is licensed under a [Creative Commons Attribution-ShareAlike 4.0 International License](https://creativecommons.org/licenses/by-sa/4.0/).

## Author Information

- [Michel Weitbrecht (SlothOfAnarchy)](https://github.com/SlothOfAnarchy) _michel.weitbrecht@stuvus.uni-stuttgart.de_
