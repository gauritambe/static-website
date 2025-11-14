# macOS / Linux (Terminal)

# Move the key to the Home directory
mv ~/Downloads/dev-keypair.pem ~/dev-keypair.pem

# Set proper file permissions (very important for SSH to work)
chmod 600 ~/dev-keypair.pem

# Verify if the key exists in the Home directory
ls -l ~/dev-keypair.pem