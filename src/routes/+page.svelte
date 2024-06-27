<script lang="ts">
    import { Button } from '$lib/components/ui/button';
    import { Input } from '$lib/components/ui/input';
    import { Select, SelectContent, SelectItem, SelectTrigger, SelectValue } from '$lib/components/ui/select';
    import { Card, CardContent, CardDescription, CardFooter, CardHeader, CardTitle } from '$lib/components/ui/card';
    import { Table, TableBody, TableCell, TableHead, TableHeader, TableRow } from '$lib/components/ui/table';

    let searchQuery = '';
    let selectedDocumentType = '';

    const documentTypes = ['Contract', 'Legal Brief', 'Court Order', 'Affidavit', 'Memorandum'];

    const mockResults = [
        { id: 1, title: 'Employment Contract', type: 'Contract', date: '2023-05-15' },
        { id: 2, title: 'Smith vs. Johnson Legal Brief', type: 'Legal Brief', date: '2023-06-02' },
        { id: 3, title: 'Restraining Order - Case #12345', type: 'Court Order', date: '2023-06-10' },
    ];
</script>

<nav class="bg-blue-900 p-4">
    <div class="container mx-auto flex justify-between items-center">
        <div class="text-white text-xl font-bold">LegalDocs Search</div>
        <div>
            <Button variant="ghost" class="text-white">Profile</Button>
            <Button variant="secondary" class="">Upload</Button>
        </div>
    </div>
</nav>

<main class="container mx-auto mt-8">
    <Card class="w-full">
        <CardHeader>
            <CardTitle>Legal Document Search</CardTitle>
            <CardDescription>Search for contracts, briefs, orders, and more.</CardDescription>
        </CardHeader>
        <CardContent>
            <div class="flex space-x-4 mb-4">
                <Input type="text" placeholder="Enter search query" bind:value={searchQuery} class="flex-grow" />
                <Select bind:value={selectedDocumentType}>
                    <SelectTrigger class="w-[180px]">
                        <SelectValue placeholder="Document Type" />
                    </SelectTrigger>
                    <SelectContent>
                        {#each documentTypes as type}
                            <SelectItem value={type}>{type}</SelectItem>
                        {/each}
                    </SelectContent>
                </Select>
                <Button>Search</Button>
            </div>

            <Table>
                <TableHeader>
                    <TableRow>
                        <TableHead>Title</TableHead>
                        <TableHead>Type</TableHead>
                        <TableHead>Date</TableHead>
                        <TableHead>Actions</TableHead>
                    </TableRow>
                </TableHeader>
                <TableBody>
                    {#each mockResults as result}
                        <TableRow>
                            <TableCell>{result.title}</TableCell>
                            <TableCell>{result.type}</TableCell>
                            <TableCell>{result.date}</TableCell>
                            <TableCell>
                                <Button variant="outline" size="sm">View</Button>
                                <Button variant="outline" size="sm" class="ml-2">Download</Button>
                            </TableCell>
                        </TableRow>
                    {/each}
                </TableBody>
            </Table>
        </CardContent>
        <CardFooter>
            <p class="text-sm text-gray-500">Showing {mockResults.length} results</p>
        </CardFooter>
    </Card>
</main>
