# iTL


# Set your backup directory
backup_dir="/path/to/backup/directory"

# Function to create a backup
create_backup() {
    # Create a timestamp for the backup folder name
    timestamp=$(date +'%Y%m%d%H%M%S')
    backup_folder="$backup_dir/backup_$timestamp"

    # Create the backup folder
    mkdir -p "$backup_folder"

    # Archive selected files/directories
    tar czvf "$backup_folder/backup.tar.gz" "${@}"

    echo "Backup created in $backup_folder"
}

# Function to restore a backup
restore_backup() {
    backup_folder="$1"
    restore_location="$2"

    if [ -f "$backup_folder/backup.tar.gz" ]; then
        tar xzvf "$backup_folder/backup.tar.gz" -

