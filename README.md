# portsnap-build

## First Time
sh -e setup.sh

cp world.tar in (magus tarball?)

sh -e keygen.sh

edit build.conf

sh -e loop.sh

## Client configuration changes

You will need to include the key from keygen in portsnap.conf for the client.  You will also need to create SRV records for the domain you include in that file in DNS for the _http.tcp 

## portsnap-cleanup.sh

The loop.sh script expects a portsnap-cleanup.sh script on the server to prune old data. Depending on the settings configured for TTL, you will need to adjust what gets cleaned. This part of portsnap isn't well documented. 

We currently believe something like find /path/to/portsnap/files  -mtime +30 -type f -print -delete  
where mtime is the number of days to go back.  Files older than 30 days ould get deleted in this example. 

## Errors
If you see errors from the client about missing snapshots, most likely the s directory on the mirrors is empty or has corrupt files. You will need to manually run a "snap" build after cleanup of the state/work directory and then get the files moved back up to the server with the upload.sh script. 
e.g.

sh -e build.sh snap 

sh upload.sh
