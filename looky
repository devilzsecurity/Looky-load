#define _GNU_SOURCE
#include <stdio.h>  // let's cook something ass
#include <stdlib.h> // for manage
#include <string.h>
#include <unistd.h>
#include <fcntl.h> // f/o
#include <dlfcn.h> // linking use

// this all is for check libc functions
const char *Libcfunctions[] = {
    "fstat", "stat", "open", "read", "write", "execve", "execveat",
    "_lxstat64", "_xstat", "_lstat" ,NULL
};

#define PATH "/etc/ld.so.preload" // now basically this macro is set to compare

// simple method to check if LD_PRELOAD in env is set to some value
void ld_env() {
    if (getenv("LD_PRELOAD")) {
        printf("[X] Warning something is there in env.!\n");
    } else {
        printf("[.] Nothing in env\n");
    }
}

void ld_file() {
    FILE *file = fopen(PATH, "r");
    if (file) {
        printf("[X] Detected there is something exist in /etc/ld.so.preload file\n");
        printf("[.] Contents in it were:\n");

        char line[256];
        while (fgets(line, sizeof(line), file)) {
            printf("%s", line);
            if (strstr(line, ".so")) {
                printf("[X] Detected something shared lib. in it : %s", line);
            }
        }
        fclose(file);
    } else {
        printf("[.] Nothing new or the file not exist of /etc/ld.so.preload....\n");
    }
}

// Simple way to check hook
void hook_checker() {
    void *handle = dlopen("libc.so.6", RTLD_LAZY);
    if (!handle) {
        printf("Failed to load libc!\n");
        return;
    }

    for (int i = 0; Libcfunctions[i]; i++) {
        void *fun_ptr = dlsym(handle, Libcfunctions[i]);
        if (fun_ptr) {
            printf("[.] Function found: %s\n", Libcfunctions[i]);
        } else {
            printf("[X] Function not found or hooked: %s\n", Libcfunctions[i]);
        }
    }
    dlclose(handle);
}

int main() {
    printf(" ========== Looky By devilzsecurity ==========\n");
    ld_env();
    ld_file();
    hook_checker();

    printf("Scan completed.......\n");

    return 0;
}
