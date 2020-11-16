int checar_usuario() {
    FILE *fp;
    char login[TAMLOGIN];
    char senha[TAMSENHA];
    Usuario usuario;
  
    printf("Autenticar usuario:\n");
    printf("Login:\n");
    scanf("%s", &login[0]);
    printf("Senha:\n");
    scanf("%s", &senha[0]);

    fp = fopen(NOME_ARQ_USUARIO, "rb");

    if (fp == NULL) {
        fprintf(stderr, "Erro ao abrir %s para leitura!\n", NOME_ARQ_USUARIO);
        exit(1);
    }

    while (!feof(fp)) {
        fread(&usuario, sizeof(Usuario), 1, fp);
        if (strncmp(&usuario.login[0], login, TAMLOGIN) == 0) {
            if (strncmp(&usuario.senha[0], senha, TAMSENHA) == 0) {
                return 1;
            }
        }
    }
    fclose(fp);
    return 0;
}

